# @Previewable을 사용하는 이유

1. **실시간 상태 변경 테스트 가능**
    - Preview에서 버튼을 클릭하거나 사용자 입력을 통해 상태 변경을 실제로 확인할 수 있다
    - 기존 `.constant()` 방식은 읽기 전용이라 상태 변경이 불가능했다
2. **실제 앱과 같은 사용자 경험 테스트**
    - 상호작용적인 Preview로 실제 앱처럼 UI 컴포넌트의 동작을 테스트할 수 있다
    - 사용자 흐름과 상태 변화에 따른 UI 업데이트를 실시간으로 확인할 수 있다
3. **개발 생산성 향상**
    - 시뮬레이터를 실행하지 않고도 UI 컴포넌트의 기능 테스트가 가능하다
    - 빠른 디버깅과 반복 개발 과정을 지원한다
4. **다양한 상태 테스트 용이성**
    - 여러 초기 상태를 쉽게 설정하고 테스트할 수 있다
    - 경계 조건과 다양한 사용자 시나리오를 Preview 내에서 확인할 수 있다
5. **다른 프로퍼티 래퍼와의 호환성**
    - `@State`, `@StateObject`, `@AppStorage`, `@SceneStorage` 등과 함께 사용 가능하다
    - 다양한 데이터 저장 방식을 Preview에서도 테스트할 수 있다

## 예시

### 1. 카운터 앱에서의 사용

swift

```swift
// CounterView.swift
struct CounterView: View {
    @Binding var count: Int
    
    var body: some View {
        VStack(spacing: 20) {
            Text("현재 카운트: \(count)")
                .font(.title)
            
            HStack(spacing: 30) {
                Button("감소") {
                    if count > 0 {
                        count -= 1
                    }
                }
                .buttonStyle(.bordered)
                
                Button("증가") {
                    count += 1
                }
                .buttonStyle(.borderedProminent)
            }
        }
        .padding()
    }
}

// Preview
#Preview {
    @Previewable @State var count = 5
    return CounterView(count: $count)
}
```

### 2. 폼 입력에서의 사용

swift

```swift
// UserProfileForm.swift
struct UserProfileForm: View {
    @Binding var username: String
    @Binding var isNotificationsEnabled: Bool
    
    var body: some View {
        Form {
            Section("프로필 정보") {
                TextField("사용자 이름", text: $username)
                
                Toggle("알림 활성화", isOn: $isNotificationsEnabled)
            }
            
            Section {
                Text("현재 설정: \(username), 알림: \(isNotificationsEnabled ? "켜짐" : "꺼짐")")
                    .font(.caption)
            }
        }
    }
}

// Preview
#Preview {
    @Previewable @State var username = "홍길동"
    @Previewable @State var notifications = true
    
    return UserProfileForm(
        username: $username,
        isNotificationsEnabled: $notifications
    )
}
```

### 3. 할 일 목록 앱에서의 사용

swift

```swift
// TodoDetailView.swift
struct TodoDetailView: View {
    @Binding var item: Item
    
    var body: some View {
        Form {
            TextField("할 일", text: $item.text)
            
            Picker("중요도", selection: $item.type) {
                ForEach(ItemType.allCases) { type in
                    Label(type.displayName, systemImage: type.icon)
                        .tag(type)
                }
            }
            
            Section("미리보기") {
                HStack {
                    Text(item.type.icon)
                    Text(item.text)
                    Spacer()
                    Text(item.type.displayName)
                        .foregroundColor(.secondary)
                }
            }
        }
        .navigationTitle("할 일 수정")
    }
}

// Preview
#Preview {
    NavigationStack {
        @Previewable @State var todoItem = Item(
            text: "SwiftUI 공부하기", 
            type: .important
        )
        
        return TodoDetailView(item: $todoItem)
    }
}
```

이러한 예시들은 `@Previewable`이 실제 개발 과정에서 어떻게 상호작용적인 UI 미리보기를 가능하게 하는지 보여준다. 개발자는 실제 앱을 실행하지 않고도 다양한 사용자 입력과 상태 변화에 따른 UI 반응을 테스트할 수 있다.

Retry

[Claude can make mistakes. Please double-check responses.](https://support.anthropic.com/en/articles/8525154-claude-is-providing-incorrect-or-misleading-responses-what-s-going-on)

  

3.7 Sonnet