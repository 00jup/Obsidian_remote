# Swift 열거형(Enumerations) 완벽 가이드

Swift의 열거형(Enumeration)은 관련된 값들의 그룹을 정의하는 방법으로, 다른 언어의 열거형보다 훨씬 강력하고 유연한 기능을 제공합니다. 이 문서에서는 Swift 열거형의 모든 특징과 사용법을 살펴보겠습니다.

## 기본 열거형 정의

가장 기본적인 형태의 열거형은 다음과 같이 정의합니다:

```swift
enum Direction {
    case north
    case south
    case east
    case west
}
```

여러 케이스를 한 줄에 콤마로 구분하여 작성할 수도 있습니다:

```swift
enum Direction {
    case north, south, east, west
}
```

## 열거형 사용하기

열거형 값을 사용할 때는 점(`.`) 구문을 사용합니다:

```swift
// 타입 명시
let myDirection: Direction = .north

// 완전한 타입 표기
let yourDirection = Direction.south

// 변수 타입이 이미 알려진 경우
var windDirection = Direction.west
windDirection = .east  // 타입 생략 가능
```

### switch 문으로 열거형 처리하기

열거형 값은 switch 문으로 완벽하게 처리할 수 있습니다:

```swift
switch myDirection {
case .north:
    print("북쪽으로 이동")
case .south:
    print("남쪽으로 이동")
case .east:
    print("동쪽으로 이동")
case .west:
    print("서쪽으로 이동")
}
```

Swift의 switch 문은 **철저함(exhaustiveness)**을 요구하므로, 모든 열거형 케이스를 처리하거나 `default` 케이스를 포함해야 합니다.

### if 문으로 열거형 처리하기

```swift
if myDirection == .north {
    print("북쪽으로 이동")
}
```

## 원시값(Raw Values)

열거형의 각 케이스에 특정 타입의 원시값을 할당할 수 있습니다:

```swift
enum HttpStatus: Int {
    case ok = 200
    case created = 201
    case accepted = 202
    case badRequest = 400
    case unauthorized = 401
    case notFound = 404
    case serverError = 500
}
```

원시값은 문자열, 문자, 정수 또는 부동소수점 숫자 타입이 될 수 있습니다.

### 원시값 자동 할당

정수 타입의 원시값은 명시적으로 지정하지 않으면 0부터 자동 증가합니다:

```swift
enum Planet: Int {
    case mercury = 1, venus, earth, mars, jupiter, saturn, uranus, neptune
    // venus=2, earth=3, ... 자동 할당
}
```

문자열 타입의 원시값은 케이스 이름과 동일한 문자열이 자동 할당됩니다:

```swift
enum CompassPoint: String {
    case north, south, east, west
    // rawValue는 "north", "south", "east", "west"
}
```

### 원시값 사용하기

```swift
// 원시값 가져오기
let statusCode = HttpStatus.notFound.rawValue  // 404

// 원시값으로부터 열거형 인스턴스 생성 (옵셔널 반환)
if let status = HttpStatus(rawValue: 404) {
    print("상태: \(status)")  // 상태: notFound
}
```

## 연관값(Associated Values)

Swift 열거형의 강력한 기능 중 하나는 각 케이스에 다른 타입의 연관값을 저장할 수 있다는 것입니다:

```swift
enum Barcode {
    case upc(Int, Int, Int, Int)
    case qrCode(String)
}
```

연관값을 포함한 열거형 값 생성:

```swift
// UPC: 시스템, 제조업체, 제품, 체크 코드
let productBarcode = Barcode.upc(8, 85909, 51226, 3)

// QR 코드: 문자열 값
let websiteQR = Barcode.qrCode("https://www.example.com")
```

### 연관값 추출하기

```swift
switch productBarcode {
case .upc(let numberSystem, let manufacturer, let product, let check):
    print("UPC: \(numberSystem), \(manufacturer), \(product), \(check)")
case .qrCode(let productCode):
    print("QR 코드: \(productCode)")
}
```

추출 문법 간소화:

```swift
switch productBarcode {
case let .upc(numberSystem, manufacturer, product, check):
    print("UPC: \(numberSystem), \(manufacturer), \(product), \(check)")
case let .qrCode(productCode):
    print("QR 코드: \(productCode)")
}
```

## 메서드와 프로퍼티

Swift의 열거형은 메서드와 계산된 프로퍼티를 가질 수 있습니다:

```swift
enum Planet {
    case mercury, venus, earth, mars, jupiter, saturn, uranus, neptune
    
    // 계산된 프로퍼티
    var description: String {
        switch self {
        case .earth:
            return "우리가 사는 행성"
        default:
            return "다른 행성"
        }
    }
    
    // 메서드
    func distanceFromSun() -> Double {
        switch self {
        case .mercury: return 57.9
        case .venus: return 108.2
        case .earth: return 149.6
        case .mars: return 227.9
        case .jupiter: return 778.3
        case .saturn: return 1427.0
        case .uranus: return 2871.0
        case .neptune: return 4497.1
        }
    }
    
    // 변경 메서드
    mutating func next() {
        switch self {
        case .mercury: self = .venus
        case .venus: self = .earth
        case .earth: self = .mars
        case .mars: self = .jupiter
        case .jupiter: self = .saturn
        case .saturn: self = .uranus
        case .uranus: self = .neptune
        case .neptune: self = .mercury
        }
    }
}

let earth = Planet.earth
print(earth.description)       // "우리가 사는 행성"
print(earth.distanceFromSun()) // 149.6

var planet = Planet.earth
planet.next()  // planet은 이제 .mars
```

## 모든 케이스 순회하기

`CaseIterable` 프로토콜을 채택하면 열거형의 모든 케이스를 순회할 수 있습니다:

```swift
enum Beverage: CaseIterable {
    case coffee, tea, juice
}

// 모든 케이스 배열 얻기
let allBeverages = Beverage.allCases
print("음료 종류: \(allBeverages.count)개")  // 음료 종류: 3개

// 모든 케이스 순회
for beverage in Beverage.allCases {
    print(beverage)
}
```

## 재귀적 열거형

열거형은 자신의 케이스 연관값으로 다시 자신을 참조할 수 있습니다. 이를 재귀적 열거형이라고 하며, `indirect` 키워드를 사용합니다:

```swift
// 전체 열거형을 재귀적으로 선언
indirect enum ArithmeticExpression {
    case number(Int)
    case addition(ArithmeticExpression, ArithmeticExpression)
    case multiplication(ArithmeticExpression, ArithmeticExpression)
}

// 또는 특정 케이스만 재귀적으로 선언
enum ArithmeticExpression {
    case number(Int)
    indirect case addition(ArithmeticExpression, ArithmeticExpression)
    indirect case multiplication(ArithmeticExpression, ArithmeticExpression)
}
```

재귀적 열거형 사용 예:

```swift
// (5 + 4) * 2 표현
let five = ArithmeticExpression.number(5)
let four = ArithmeticExpression.number(4)
let sum = ArithmeticExpression.addition(five, four)
let product = ArithmeticExpression.multiplication(sum, ArithmeticExpression.number(2))

// 재귀적 열거형 계산 함수
func evaluate(_ expression: ArithmeticExpression) -> Int {
    switch expression {
    case let .number(value):
        return value
    case let .addition(left, right):
        return evaluate(left) + evaluate(right)
    case let .multiplication(left, right):
        return evaluate(left) * evaluate(right)
    }
}

print(evaluate(product))  // 18
```

## 패턴 매칭과 열거형

Swift의 패턴 매칭을 사용하면 열거형 값을 더 유연하게 처리할 수 있습니다:

```swift
// 부분 패턴 매칭
let point = (2, 0)

switch point {
case (let x, 0):
    print("x축 위의 점: \(x)")
case (0, let y):
    print("y축 위의 점: \(y)")
case let (x, y):
    print("다른 점: (\(x), \(y))")
}

// 열거형에서의 where 절 사용
enum Temperature {
    case celsius(Double)
    case fahrenheit(Double)
}

let temp = Temperature.celsius(25)

switch temp {
case .celsius(let t) where t > 30:
    print("매우 더움: \(t)°C")
case .celsius(let t) where t < 0:
    print("얼음점 이하: \(t)°C")
case .celsius(let t):
    print("온도: \(t)°C")
case .fahrenheit(let t) where t > 86:
    print("매우 더움: \(t)°F")
case .fahrenheit(let t):
    print("온도: \(t)°F")
}
```

## 메모리 최적화

Swift의 열거형은 메모리 효율적입니다. 원시값이 없는 열거형은 필요한 최소한의 메모리만 사용합니다:

```swift
// 최적화된 메모리 사용
enum Direction {
    case north, south, east, west
}
// 2비트만 필요 (4가지 경우를 표현하기 위해)

// 명시적 메모리 레이아웃 지정
enum Alignment: Int8 {
    case left = 0
    case center = 1
    case right = 2
}
// Int8 크기만큼 사용 (1바이트)
```

## 실제 사용 사례

### 옵셔널 타입

Swift의 `Optional` 타입은 사실 열거형으로 구현되어 있습니다:

```swift
enum Optional<Wrapped> {
    case none
    case some(Wrapped)
}
```

### 결과 타입

작업의 성공 또는 실패를 나타내는 `Result` 타입도 열거형입니다:

```swift
enum Result<Success, Failure: Error> {
    case success(Success)
    case failure(Failure)
}
```

### 상태 관리

앱의 상태를 관리할 때 열거형이 유용합니다:

```swift
enum NetworkState {
    case idle
    case loading
    case success(Data)
    case failure(Error)
}

enum ViewState {
    case loading
    case content([Item])
    case empty
    case error(String)
}
```

### 명령 패턴

사용자 작업이나 시스템 명령을 나타낼 때 유용합니다:

```swift
enum EditorCommand {
    case createNewFile(name: String)
    case openFile(url: URL)
    case saveFile
    case closeFile
    case cut(Range<Int>)
    case copy(Range<Int>)
    case paste(position: Int, content: String)
}
```

### API 응답 처리

서버 응답을 타입 안전하게 처리할 수 있습니다:

```swift
enum APIResponse<T: Decodable> {
    case success(T)
    case error(statusCode: Int, message: String)
    case networkError(Error)
    case decodingError(Error)
}
```

Swift의 열거형은 이처럼 다양한 상황에서 타입 안전성과 코드 가독성을 높이는 데 큰 도움이 됩니다.