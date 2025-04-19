부모 컴포넌트에서 바인딩 값을 `false`로 전달받은 후 자식 컴포넌트에서 이 값을 `true`로 변경하려면 간단하게 `playing = true` 구문을 사용하면 된다.

예를 들어:

```swift
struct MusicControlButton: View {
    @Binding var playing: Bool
    
    var body: some View {
        Button(action: {
            // 바인딩 값을 true로 변경
            playing = true
            
            // 추가 작업 수행
            AudioManager.shared.startPlayer(track: "songName")
        }) {
            Image(systemName: playing ? "pause.circle.fill" : "play.circle.fill")
        }
    }
}
```

이렇게 하면 바인딩된 값이 변경되고, 그 변경은 부모 컴포넌트에도 반영된다. `@Binding`의 목적이 바로 이것이다 - 자식 컴포넌트에서 변경한 값이 부모 컴포넌트의 상태에 반영되도록 하는 것.

또한 `onAppear` 수정자를 사용하여 뷰가 나타날 때 값을 변경할 수도 있다:

```swift
struct MusicControlButton: View {
    @Binding var playing: Bool
    
    var body: some View {
        Button(action: { 
            // 버튼 액션
        }) {
            // 버튼 레이블
        }
        .onAppear {
            // 뷰가 처음 나타날 때 playing을 true로 설정
            playing = true
        }
    }
}
```

이 방식은 뷰가 화면에 나타나자마자 바인딩 값을 변경하고 싶을 때 유용하다.