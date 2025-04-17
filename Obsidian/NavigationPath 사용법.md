# 📘 SwiftUI NavigationPath를 이용한 화면 전환 완전 가이드

> 이 문서는 `SwiftUI`에서 `NavigationPath`를 활용한 화면 전환 방식을 정리한 것이다.  
> 여러 개의 뷰 파일 간 데이터 기반 화면 이동을 명확하게 구현할 수 있도록 예제와 함께 설명한다.  
> 📅 작성일: 2025년 4월

---

## 📂 프로젝트 구조

Project
├─ Views
│   ├─ ContentView.swift        // 메인 NavigationStack
│   ├─ FirstView.swift          // 목적지 1
│   └─ SecondView.swift         // 목적지 2
│
└─ Models
└─ Route.swift              // 목적지 enum

---

## 🔸 Route.swift - 목적지 정의

```swift
// Route.swift
import Foundation

enum Route: Hashable {
    case firstView(String)    // 메시지 전달용
    case secondView(Int)      // 숫자 전달용
}
```



---
## 🔸 ContentView.swift - 메인 화면 + 경로 관리

// ContentView.swift

```swift
import SwiftUI

struct ContentView: View {
    @State private var path = NavigationPath()

    var body: some View {
        NavigationStack(path: $path) {
            VStack(spacing: 20) {
                Button("Go to First View") {
                    path.append(Route.firstView("Hello First"))
                }
                Button("Go to Second View") {
                    path.append(Route.secondView(42))
                }
            }
            .navigationTitle("Main View")
            .navigationDestination(for: Route.self) { route in
                switch route {
                case .firstView(let msg):
                    FirstView(message: msg, path: $path)
                case .secondView(let number):
                    SecondView(number: number, path: $path)
                }
            }
        }
    }
}
```
---
## 🔸 FirstView.swift - 메시지를 받는 목적지

```swift
// FirstView.swift
import SwiftUI

struct FirstView: View {
    let message: String
    @Binding var path: NavigationPath

    var body: some View {
        VStack(spacing: 20) {
            Text("📄 First View")
            Text("Message: \(message)")

            Button("Go to Second View") {
                path.append(Route.secondView(100))
            }

            Button("Back to Main") {
                path.removeLast(path.count)
            }
        }
        .navigationTitle("First View")
    }
}
```

---

## 🔸 SecondView.swift - 숫자를 받는 목적지

```swift
// SecondView.swift
import SwiftUI

struct SecondView: View {
    let number: Int
    @Binding var path: NavigationPath

    var body: some View {
        VStack(spacing: 20) {
            Text("📄 Second View")
            Text("Number: \(number)")

            Button("Go to First View") {
                path.append(Route.firstView("Second에서 이동"))
            }

            Button("Back to Main") {
                path.removeLast(path.count)
            }
        }
        .navigationTitle("Second View")
    }
}
```

```

📌 NavigationPath의 핵심 개념 요약

개념	설명
NavigationPath	경로를 배열처럼 관리, 화면 전환을 중앙에서 제어
Route enum	각 화면 목적지를 enum으로 정의 (데이터 포함 가능)
.navigationDestination	경로에 맞는 목적지를 렌더링하는 뷰 매핑
path.append(...)	특정 뷰로 이동 (데이터와 함께)
path.removeLast()	한 단계 뒤로 가기
path.removeLast(path.count)	메인 뷰로 돌아가기 (전체 초기화)



⸻

🤔 왜 데이터를 같이 넘기는가?
	•	뷰에서 로직이나 표시 내용을 상황에 따라 바꾸기 위해
	•	예: 로그인 → Welcome 메시지 전달 / 사용자 ID 기반 프로필 화면

path.append(Route.firstView("로그인 성공!"))

➡ 해당 메시지를 FirstView에서 받아서 화면에 표시하거나 처리할 수 있다.

⸻

✅ 요약
	•	NavigationPath + Route enum 조합은 복잡한 화면 전환을 깔끔하게 구성할 수 있게 해준다.
	•	뷰 간 데이터 전달도 자연스럽고 명확하게 할 수 있다.
	•	각각의 뷰는 독립 파일로 분리하며, 중앙에서 경로를 제어하면 유지보수도 편하다.

⸻

📎 참고: SwiftUI 4.0 이상에서 사용 가능
📚 Apple 공식 문서: NavigationStack - SwiftUI Documentation

