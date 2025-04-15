Swift에서 `:` 콜론 뒤에 오는 것들의 의미는 상황에 따라 다르다:

### enum 뒤의 콜론

1. **원시값 타입 지정**:

```swift
enum Direction: String {
    case north, south, east, west
}
```

여기서 `String`은 원시값의 타입이다.

2. **프로토콜 채택**:

```swift
enum Direction: CaseIterable {
    case north, south, east, west
}
```

여기서 `CaseIterable`은 채택한 프로토콜이다.

### class 뒤의 콜론

1. **상속**:

```swift
class ChildClass: ParentClass {
    // 구현 내용
}
```

여기서 `ParentClass`는 상속받는 부모 클래스다.

2. **프로토콜 채택**:

```swift
class MyClass: SomeProtocol {
    // 프로토콜 요구사항 구현
}
```

3. **상속과 프로토콜 채택 동시에**:

```swift
class MyViewController: UIViewController, UITableViewDelegate {
    // 구현 내용
}
```

### struct 뒤의 콜론

```swift
struct MyStruct: ProtocolA, ProtocolB {
    // 구현 내용
}
```

여기서는 상속이 불가능하므로 항상 프로토콜 채택이다.

### func 뒤의 콜론

함수 정의에서 콜론(`:`)은 매개변수 이름과 타입을 구분하는 데 사용된다:

```swift
func greet(person: String) -> String {
    return "Hello, " + person
}
```

따라서 `:` 콜론 뒤에 오는 것들은 항상 프로토콜이 아니라 문맥에 따라 의미가 달라진다:

- 원시값 타입 (enum)
- 상속받을 부모 클래스 (class)
- 채택할 프로토콜(들) (enum, class, struct)
- 매개변수 타입 (func)

여러 프로토콜을 채택할 경우 콤마(`,`)로 구분한다.