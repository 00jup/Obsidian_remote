# Swift의 옵셔널 연산자: `?`와 `??`

Swift에서 옵셔널 관련 연산자인 `?`와 `??`는 서로 다른 목적과 기능을 가지고 있습니다. 이 두 연산자의 차이점과 사용법을 살펴보겠습니다.

## `?` 연산자 (옵셔널 타입 선언 및 옵셔널 체이닝)

### 1. 옵셔널 타입 선언

`?`는 변수나 상수가 값을 가질 수도 있고, 값이 없을 수도 있음을 나타냅니다.

```swift
// 옵셔널 String 타입 선언
var name: String? = "Swift"
name = nil // nil 할당 가능

// 옵셔널이 아닌 타입에는 nil 할당 불가
var nonOptionalName: String = "Swift"
// nonOptionalName = nil // 컴파일 에러
```

### 2. 옵셔널 체이닝 (Optional Chaining)

`?`는 옵셔널 값이 nil이 아닐 경우에만 그 다음 속성이나 메소드에 접근할 수 있게 해줍니다.

```swift
struct Person {
    var name: String
    var address: Address?
}

struct Address {
    var street: String
    var city: String
}

let person: Person? = Person(name: "John", address: Address(street: "123 Main St", city: "Seoul"))

// 옵셔널 체이닝
let city = person?.address?.city // "Seoul"

// person이 nil이면 전체 표현식이 nil이 됨
let anotherPerson: Person? = nil
let anotherCity = anotherPerson?.address?.city // nil
```

### 3. 옵셔널 바인딩 (Optional Binding)

`if let` 또는 `guard let`과 함께 사용하여 옵셔널 값을 안전하게 언래핑합니다.

```swift
if let unwrappedName = name {
    print("이름은 \(unwrappedName)입니다")
} else {
    print("이름이 없습니다")
}

// Swift 5.7부터 더 간결한 문법
if let name {
    print("이름은 \(name)입니다")
}
```

## `??` 연산자 (Nil-coalescing Operator)

`??`는 옵셔널 값이 nil일 경우 기본값을 제공하는 연산자입니다.

### 1. 기본 사용법

```swift
let optionalValue: Int? = nil
let defaultValue = 10

// optionalValue가 nil이므로 defaultValue인 10이 할당됨
let result = optionalValue ?? defaultValue // 10

let anotherOptionalValue: Int? = 5
// anotherOptionalValue가 nil이 아니므로 5가 할당됨
let anotherResult = anotherOptionalValue ?? defaultValue // 5
```

### 2. 체이닝 사용

여러 옵셔널 값 중 첫 번째 non-nil 값을 선택할 수 있습니다.

```swift
let first: String? = nil
let second: String? = nil
let third: String? = "Hello"
let defaultString = "Default"

let value = first ?? second ?? third ?? defaultString // "Hello"
```

### 3. 옵셔널 체이닝과 함께 사용

```swift
let cityName = person?.address?.city ?? "Unknown City"
```

## 두 연산자의 차이점

| 특징    | `?`                | `??`           |
| ----- | ------------------ | -------------- |
| 목적    | 옵셔널 타입 선언 및 안전한 접근 | nil일 경우 기본값 제공 |
| 사용 위치 | 타입 선언, 속성/메소드      |                |