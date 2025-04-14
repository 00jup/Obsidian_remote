# Swift 바인딩과 SwiftUI Preview 사용법

## 기본 자료구조

```swift
enum ItemType: String, CaseIterable, Identifiable {
    case normal
    case important
    case reminder
    
    var id: String { self.rawValue }
    
    var icon: String {
        switch self {
        case .normal: return "📝"
        case .important: return "❗️"
        case .reminder: return "⏰"
        }
    }
    
    var displayName: String {
        switch self {
        case .normal: return "일반"
        case .important: return "중요"
        case .reminder: return "리마인더"
        }
    }
}

struct Item: Identifiable {
    let id = UUID()
    var text: String
    var type: ItemType = .normal
}
```

이 코드는 to-do 리스트 앱에 사용될 수 있는 자료구조를 정의하며:
- `ItemType` 열거형: 일반, 중요, 리마인더 세 가지 유형의 항목을 정의
- `Item` 구조체: 고유 ID, 텍스트 내용, 항목 유형을 가진 개별 항목 표현

## SwiftUI에서 Binding 사용하기

### SubView 정의

```swift
import SwiftUI

struct SubView: View {
    @Binding var count: Int
    
    var body: some View {
        VStack {
            Text("\(count)")
            
            Button{
                count -= 1
            } label: {
                Text("Minus Yoshi")
            }
        }
    }
}
```

### ContentView 정의

```swift
import SwiftUI

struct ContentView: View {
    @State var count: Int = 0
    
    var body: some View {
        NavigationStack{
            VStack {
                Text("\(count)")
                
                Button{
                    count += 1
                } label: {
                    Text("Plus Yoshi")
                }
            }
            NavigationLink{
                SubView(count: $count)
            } label: {
                Text("더하기")
            }
        }
    }
}
```

## Preview 사용 방법들

### 1. `.constant()` 사용하기 (모든 SwiftUI 버전)

읽기 전용 바인딩을 생성하여 레이아웃만 확인 가능:

```swift
#Preview {
    SubView(count: .constant(2))
}
```

### 2. 매개변수 레이블 제거하기

매개변수 이름 없이 호출할 수 있게 초기화 메서드 변경:

```swift
struct SubView: View {
    @Binding var count: Int
    
    // 매개변수 레이블을 제거한 초기화 메서드
    init(_ count: Binding<Int>) {
        self._count = count
    }
    
    // 나머지 코드는 동일
}

#Preview {
    SubView(.constant(2))  // 매개변수 이름 없이 사용
}
```

### 3. 기본 매개변수 추가하기

Preview용 기본값 설정:

```swift
struct SubView: View {
    @Binding var count: Int
    
    // Preview용 초기화 메서드 추가
    init(count: Binding<Int> = .constant(2)) {
        self._count = count
    }
    
    // 나머지 코드는 동일
}

#Preview {
    SubView()  // 매개변수 없이 사용 가능
}
```

### 4. @Previewable 사용하기 (SwiftUI 5.0, iOS 18+)

Preview에서 상태 변경이 가능한 방법:

```swift
#Preview {
    @Previewable @State var count = 3
    SubView(count: $count)
}
```

`@Previewable`은 다음 프로퍼티 래퍼들과 함께 사용 가능:
- `@State`: 간단한 값 타입을 위한 상태
- `@StateObject`: 참조 타입(클래스)을 위한 상태
- `@AppStorage`: UserDefaults에 저장되는 값
- `@SceneStorage`: 씬별 상태 저장

## @Previewable의 장점

1. Preview에서 상태 변경이 가능함 (버튼 클릭 시 실제로 값이 변경됨)
2. 실제 앱처럼 상호작용을 테스트할 수 있음
3. Preview 단계에서 기능 테스트가 가능함

## 정리

- SwiftUI에서 부모-자식 뷰 간 데이터 공유는 `@State`와 `@Binding`을 통해 이루어짐
- Preview에서 `@Binding` 매개변수를 사용하는 뷰를 테스트하는 여러 방법이 있음
- iOS 18 이상에서는 `@Previewable`을 사용하여 Preview에서도 실제 상호작용 테스트가 가능함