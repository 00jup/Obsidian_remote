![[Pasted image 20250422105641.png]]

경고에서 볼 수 있듯이 `onChange(of:perform:)` 메서드가 iOS 17.0에서 deprecated(폐지 예정)되었다. 이는 SwiftUI에서 값의 변화를 관찰하는 방식이 업데이트되었기 때문이다.

대신에 새로운 `onChange(of:)` 메서드를 사용해야 한다. 새 메서드는 클로저의 매개변수 구조가 다르며, 이전 값과 새 값 모두에 접근할 수 있다:

```swift
.onChange(of: volume) { oldValue, newValue in
    AudioManager.shared.setVolume(volume: Float(newValue))
}
```

이 새로운 구문은 더 명확하고 유용하다. 이전 값과 새 값 모두에 접근할 수 있어 두 값을 비교할 수도 있다. 물론 이전 값이 필요 없다면 와일드카드(`_`)로 대체할 수 있다:

```swift
.onChange(of: volume) { _, newValue in
    AudioManager.shared.setVolume(volume: Float(newValue))
}
```

새 메서드를 사용하면 경고가 사라지고 앱이 미래 iOS 버전과의 호환성을 유지하게 된다.