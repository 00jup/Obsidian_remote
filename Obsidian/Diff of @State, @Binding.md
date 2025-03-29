# SwiftUI에서의 @State와 @Binding 이해하기

## 핵심 개념 요약

SwiftUI에서 화면 간 데이터를 공유하고 관리하는 두 가지 핵심 도구가 있다:

- **@State**: 데이터의 원본 소유자
- **@Binding**: 데이터 원본에 대한 참조 연결

## 실생활 비유로 이해하기

**@State**는 집의 실제 전등 스위치와 같다. 스위치를 올리면 불이 켜지고 내리면 불이 꺼진다. 이 스위치는 전등을 직접 제어하는 원본 제어장치다.

**@Binding**은 같은 전등을 제어하는 리모컨과 같다. 리모컨으로 불을 켜고 끌 수 있지만, 리모컨 자체는 전등을 소유하지 않는다. 원래 스위치의 상태를 변경할 수 있는 연결된 장치일 뿐이다.

## 화면 A, B, C 사이의 데이터 흐름 예시

### 상황 설명

- **화면 A**: 앱의 메인 화면으로, 사용자 정보를 관리
- **화면 B**: A 내부에 표시되는 프로필 카드 컴포넌트
- **화면 C**: 프로필 편집을 위해 새로 열리는 화면

### 코드로 보는 예시

#### 화면 A (메인 화면)

```swift
struct ScreenA: View {
    // 사용자 이름을 관리하는 원본 데이터 (전등 스위치)
    @State private var username = "홍길동"
    
    var body: some View {
        VStack {
            Text("안녕하세요, \(username)님!")
                .font(.title)
            
            // 화면 B에 username 바인딩 전달
            ScreenB(displayName: $username)
            
            // 화면 C로 이동하는 버튼
            NavigationLink("프로필 편집") {
                ScreenC(username: $username)
            }
            .buttonStyle(.borderedProminent)
        }
        .padding()
    }
}
```

#### 화면 B (프로필 카드)

```swift
struct ScreenB: View {
    // A에서 전달받은 이름에 대한 참조 (리모컨)
    @Binding var displayName: String
    
    var body: some View {
        VStack {
            Image(systemName: "person.circle")
                .font(.system(size: 80))
            
            Text(displayName)
                .font(.headline)
            
            // 간단한 수정 버튼 (이것도 원본 데이터를 변경할 수 있음)
            Button("'님' 추가") {
                if !displayName.hasSuffix("님") {
                    displayName += "님"
                }
            }
        }
        .padding()
        .background(Color.gray.opacity(0.1))
        .cornerRadius(10)
    }
}
```

#### 화면 C (편집 화면)

```swift
struct ScreenC: View {
    // A에서 전달받은 이름에 대한 참조 (또 다른 리모컨)
    @Binding var username: String
    
    // 이 화면 내에서만 사용되는 임시 입력값 (완전히 별개의 전등과 스위치)
    @State private var tempUsername = ""
    
    var body: some View {
        VStack {
            Text("프로필 편집")
                .font(.title)
                .padding()
            
            Text("현재 이름: \(username)")
            
            TextField("새 이름 입력", text: $tempUsername)
                .textFieldStyle(.roundedBorder)
                .padding()
            
            Button("저장") {
                // 임시값을 원본에 반영 (리모컨으로 원래 스위치 조작)
                if !tempUsername.isEmpty {
                    username = tempUsername
                }
            }
            .buttonStyle(.borderedProminent)
        }
        .padding()
        .onAppear {
            // 화면이 나타날 때 현재 이름을 임시 입력값에 복사
            tempUsername = username
        }
    }
}
```

## 데이터 흐름 설명

1. **화면 A**가 `username`이라는 @State 변수를 소유하고 있다.
    
    - 이것은 데이터의 원본이며, 모든 변경사항의 소스다
    - A는 이 값을 직접 읽고 수정할 수 있다
2. **화면 B**는 A의 `username`에 대한 @Binding을 받는다:
    
    - B는 이 값을 읽고 수정할 수 있지만, 소유하지는 않는다
    - B에서 `displayName`을 변경하면 A의 `username`도 실시간으로 변경된다
    - A와 B 모두 업데이트된 값을 보게 된다
3. **화면 C**는 네비게이션으로 이동한 별도 화면이지만:
    
    - 여전히 A의 `username`에 대한 @Binding을 가진다
    - 사용자가 새 이름을 입력하고 저장하면 A의 원본 데이터가 업데이트된다
    - C에서는 `tempUsername`이라는 자체 @State도 가지고 있는데, 이는 C 내부에서만 사용된다
    - 사용자가 저장 버튼을 누르기 전까지는 A의 데이터에 영향을 주지 않는다

## $ 기호의 의미

코드에서 `$username`과 같이 $를 붙이는 것은 "이 State 변수에 대한 Binding을 만들어줘"라고 요청하는 것이다.

```swift
// 이것은 값 자체를 전달 (읽기만 가능)
ScreenB(displayName: username)

// 이것은 값에 대한 참조를 전달 (읽고 쓰기 가능)
ScreenB(displayName: $username)
```

## 요약

- **@State**는 데이터의 원본 소유자다 (화면 A의 username)
- **@Binding**은 다른 곳에서 소유한 데이터에 대한 참조다 (화면 B와 C가 A의 데이터를 사용)
- 상태가 변경되면 해당 상태를 사용하는 모든 화면이 자동으로 업데이트된다
- $기호를 사용하여 @State 변수의 바인딩을 생성한다

이 개념을 이해하면 복잡한 SwiftUI 앱에서도 화면 간 데이터 공유와 상태 관리를 효과적으로 할 수 있다.