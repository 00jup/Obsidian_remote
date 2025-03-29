# VStack과 LazyVStack 비교

SwiftUI에서 제공하는 두 가지 수직 스택 컨테이너인 `VStack`과 `LazyVStack`은 비슷해 보이지만 중요한 차이점이 있다. 이 글에서는 두 컴포넌트의 특징, 차이점, 그리고 언제 어떤 것을 사용해야 하는지 알아보자.

## VStack

### 특징

- **즉시 로딩**: 모든 하위 뷰를 한 번에 메모리에 로드하고 렌더링한다.
- **크기 계산**: 모든 하위 뷰의 크기를 미리 계산한다.
- **정렬 옵션**: 수평 정렬(alignment)과 간격(spacing)을 지정할 수 있다.
- **iOS 13부터 지원**: SwiftUI가 처음 소개된 시점부터 사용 가능하다.

### 코드 예시

```swift
VStack(alignment: .leading, spacing: 10) {
    Text("제목")
        .font(.title)
    Text("부제목")
        .font(.subheadline)
    Text("본문...")
}
```

## LazyVStack

### 특징

- **지연 로딩**: 화면에 보이는 뷰만 메모리에 로드하고 렌더링한다.
- **필요 시 계산**: 뷰가 화면에 표시될 때만 크기를 계산한다.
- **스크롤 컨테이너 내부**: 주로 `ScrollView` 내부에서 사용된다.
- **정렬 옵션**: VStack과 동일하게 정렬과 간격 지정이 가능하다.
- **iOS 14부터 지원**: iOS 14에서 추가된 기능이다.
- **핀 지원**: `pinToScrollableEdges` 매개변수를 통해 스크롤 가장자리에 뷰를 고정할 수 있다.

### 코드 예시

```swift
ScrollView {
    LazyVStack(alignment: .leading, spacing: 10) {
        ForEach(0..<1000) { index in
            Text("항목 \(index)")
                .padding()
        }
    }
}
```

## 주요 차이점

1. **메모리 관리**
    
    - VStack: 모든 하위 뷰를 메모리에 유지하므로 항목이 많을 경우 많은 메모리를 사용한다.
    - LazyVStack: 화면에 보이는 뷰만 메모리에 로드하므로 메모리 사용량이 효율적이다.
2. **성능**
    
    - VStack: 항목이 적을 때 더 효율적일 수 있다.
    - LazyVStack: 많은 항목을 표시할 때 성능이 더 좋다.
3. **뷰 상태 유지**
    
    - VStack: 항상 모든 뷰의 상태를 유지한다.
    - LazyVStack: 화면에서 사라진 뷰는 메모리에서 해제될 수 있어 상태가 초기화될 수 있다.
4. **렌더링 동작**
    
    - VStack: 모든 하위 뷰를 한 번에 렌더링한다.
    - LazyVStack: 필요한 뷰만 렌더링하므로 초기 렌더링 시간이 짧다.
5. **사용 컨텍스트**
    
    - VStack: 독립적으로 사용 가능하다.
    - LazyVStack: 주로 `ScrollView` 내부에서 사용하며, 스크롤 가능한 컨텐츠에 적합하다.

## 언제 어떤 것을 사용해야 할까?

### VStack 사용 시나리오

- 적은 수의 정적 뷰(10개 미만)를 표시할 때
- 모든 항목이 항상 표시되어야 할 때
- 하위 뷰가 복잡하지 않고 메모리 사용량이 적을 때
- 하위 뷰의 상태가 항상 유지되어야 할 때

### LazyVStack 사용 시나리오

- 많은 수의 항목(10개 이상)을 표시할 때
- 동적 콘텐츠나 데이터 목록을 표시할 때
- 사용자가 스크롤하여 더 많은 콘텐츠를 볼 수 있을 때
- 메모리 사용량과 성능 최적화가 중요할 때
- 초기 렌더링 시간을 최소화해야 할 때

## 코드 비교 예시

### VStack 예시

```swift
struct ContentView: View {
    var body: some View {
        VStack {
            ForEach(0..<20) { index in
                Text("항목 \(index)")
                    .padding()
                    .frame(maxWidth: .infinity)
                    .background(Color.gray.opacity(0.2))
                    .cornerRadius(8)
            }
        }
        .padding()
    }
}
```

### LazyVStack 예시

```swift
struct ContentView: View {
    var body: some View {
        ScrollView {
            LazyVStack {
                ForEach(0..<1000) { index in
                    Text("항목 \(index)")
                        .padding()
                        .frame(maxWidth: .infinity)
                        .background(Color.gray.opacity(0.2))
                        .cornerRadius(8)
                }
            }
            .padding()
        }
    }
}
```

## 성능 최적화 팁

### VStack 최적화

- 가능한 한 적은 수의 하위 뷰만 포함시킨다.
- 복잡한 뷰는 별도의 컴포넌트로 분리한다.
- `@ViewBuilder`를 사용하여 조건부 콘텐츠를 효율적으로 관리한다.

### LazyVStack 최적화

- 각 셀의 복잡성을 최소화한다.
- 이미지와 같은 무거운 리소스는 지연 로딩한다.
- 재사용 가능한 뷰를 사용하여 메모리 사용량을 줄인다.
- `id` 매개변수를 사용하여 뷰 식별을 최적화한다.

## 결론

`VStack`과 `LazyVStack`은 각각 다른 사용 사례에 최적화되어 있다. 적은 수의 정적 항목을 표시할 때는 `VStack`이 적합하고, 많은 수의 동적 항목을 효율적으로 표시할 때는 `LazyVStack`이 더 나은 선택이다. 앱의 성능과 메모리 사용량을 최적화하려면 적절한 상황에 맞는 컴포넌트를 선택하는 것이 중요하다.