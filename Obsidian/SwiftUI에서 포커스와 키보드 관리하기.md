## @FocusState와 focused 수식어의 이해

### @FocusState 속성

`@FocusState`는 SwiftUI에서 포커스 상태를 관리하는 속성 래퍼다. 이를 사용해 어떤 컨트롤이 현재 포커스를 가지고 있는지 추적할 수 있다.

```swift
@FocusState var leftTyping: Bool
@FocusState var rightTyping: Bool
```

이 속성의 특징:

- `leftTyping`이 true면 연결된 요소가 포커스를 가진다
- `rightTyping`이 true면 해당 요소가 포커스를 가진다
- 프로그래밍 방식으로 이 값을 변경하면 UI의 포커스도 같이 변경된다

### focused 수식어

`.focused()` 수식어는 텍스트 필드와 같은 입력 컨트롤에 적용해 해당 컨트롤을 `@FocusState` 변수와 연결한다.

```swift
TextField("Amount", text: $leftAmount)
    .textFieldStyle(.roundedBorder)
    .focused($leftTyping)
```

작동 방식:

- 텍스트 필드가 포커스를 받으면 `leftTyping`이 자동으로 true가 된다
- 코드에서 `leftTyping`을 true로 설정하면 텍스트 필드가 포커스를 받는다
- `leftTyping`을 false로 설정하면 텍스트 필드가 포커스를 잃고 키보드가 내려간다

## 실제 사용 사례

### 키보드 내리기 함수

```swift
func dismissKeyboard() {
    leftTyping = false
    rightTyping = false
}
```

이 함수는 모든 텍스트 필드의 포커스를 제거해 키보드를 내린다.

### 이미지 탭으로 키보드 내리기

```swift
Image(.prancingpony)
    .resizable()
    .scaledToFit()
    .frame(height: 200)
    .onTapGesture {
        if leftTyping || rightTyping {
            dismissKeyboard()
        }
    }
```

사용자가 이미지를 탭하면 키보드가 활성화된 상태일 때 키보드를 내린다.

### 배경 탭으로 키보드 내리기 (추가 가능)

```swift
ZStack {
    // 배경 이미지
    Image(.background)
        .resizable()
        .ignoresSafeArea()
        .contentShape(Rectangle())
        .onTapGesture {
            dismissKeyboard()
        }
    
    // 나머지 콘텐츠
}
```

## focused가 없을 때의 문제점

focused 수식어가 없으면:

- 텍스트 필드를 탭하면 여전히 키보드는 나타나지만
- 프로그래밍 방식으로 포커스를 제어할 수 없다
- 사용자가 화면의 다른 곳을 탭하거나 시스템 제스처를 사용하는 것 외에는 키보드를 내릴 방법이 없다
- 더 복잡한 포커스 관리(예: 다음 필드로 자동 이동)를 구현할 수 없다

## 더 많은 포커스 관리 기능

### 키보드에 완료 버튼 추가

```swift
.toolbar {
    ToolbarItemGroup(placement: .keyboard) {
        Spacer()
        Button("완료") {
            dismissKeyboard()
        }
    }
}
```

### 다중 필드 사이 포커스 이동

여러 필드 간에 포커스를 이동할 때는 열거형을 사용할 수 있다:

```swift
enum Field {
    case leftAmount
    case rightAmount
}

@FocusState private var focusedField: Field?

// 사용
TextField("Amount", text: $leftAmount)
    .focused($focusedField, equals: .leftAmount)

// 다음 필드로 이동
Button("다음") {
    focusedField = .rightAmount
}
```

이렇게 `@FocusState`와 `focused` 수식어를 활용하면 더 나은 사용자 경험을 위한 키보드 관리가 가능하다.