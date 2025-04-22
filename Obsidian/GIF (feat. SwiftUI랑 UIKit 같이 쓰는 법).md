```shell
## 파일 디렉토리로 찾아가서
pod init
## if 없다면 install
## with homebrew..
vim Podfile
## 내부 ios version 바꾸기
## 그리고 
pod 'Gifu'
## 추가 후
pod install
```

sandbox 오류가 나오면 User Script Sandboxing No로 하면 됨
![[Pasted image 20250422085726.png]]
## 코드
```swift
// CustomLoading.swift
// mazeLearner
// Created by 박정욱 on 4/15/25.

import UIKit
import Gifu

class CustomLoading {
    private static let shared = CustomLoading()
    private var backgroundView: UIView?
    private var popupView: GIFImageView?

    class func show() {
        let backgroundView = UIView()
        let popupView = GIFImageView()

        // iOS 13 이상에서 사용하는 방식
        if let windowScene = UIApplication.shared.connectedScenes.first as? UIWindowScene,
           let window = windowScene.windows.first(where: { $0.isKeyWindow }) {
            window.addSubview(backgroundView)
            window.addSubview(popupView)

            backgroundView.frame = CGRect(x: 0, y: 0, width: window.frame.maxX, height: window.frame.maxY)
            backgroundView.backgroundColor = UIColor(red: 0, green: 0, blue: 0, alpha: 0.4)

            popupView.frame = CGRect(x: 0, y: 0, width: 50, height: 50)
            popupView.translatesAutoresizingMaskIntoConstraints = false

            NSLayoutConstraint.activate([
                popupView.centerYAnchor.constraint(equalTo: window.centerYAnchor),
                popupView.centerXAnchor.constraint(equalTo: window.centerXAnchor),
                popupView.widthAnchor.constraint(equalToConstant: 50),
                popupView.heightAnchor.constraint(equalToConstant: 50)
            ])

            popupView.animate(withGIFNamed: "miro")

            shared.backgroundView?.removeFromSuperview()
            shared.popupView?.removeFromSuperview()

            shared.backgroundView = backgroundView
            shared.popupView = popupView
        }
    }

    class func hide() {
        if let popupView = shared.popupView, let backgroundView = shared.backgroundView {
            popupView.stopAnimatingGIF()
            backgroundView.removeFromSuperview()
            popupView.removeFromSuperview()
        }
    }
}
```

## 사용법
싱글톤이라서 그대로 가져다 쓰면 됨
```swift
CustomLoading.show()
CustomLoading.hide()

DispatchQueue.main.asyncAfter(deadline: .now() + 1.0) {
		CustomLoading.hide()
	}
```

