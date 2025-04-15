## Swift에서 사용자 정의 타입 배열 선언

1. **타입 정의**
    ```
    struct Person {
        var name: String
        var age: Int
    }
    ```

2. **배열 선언 및 초기화**
    ```
    var a: [Person] = [
        Person(name: "철수", age: 20),
        Person(name: "영희", age: 22)
    ]
    ```

3. **빈 배열 선언**
    ```
    var a: [Person] = []
    ```

---

## 배열 선언의 신기한 방법

- **Array(repeating:count:)로 값 반복**
    ```
    var arr = [Int](repeating: 0, count: 3) //
    var arr2 = Array(repeating: "A", count: 5) // ["A", "A", "A", "A", "A"]
    ```

- **Any 타입으로 여러 타입 혼합**
    ```
    var mixedArray: [Any] = [1, "문자열", 3.14, true]
    ```

- **타입 추론 활용**
    ```
    var arr = [1,Int 배열
    var arr2 = ["a", "b", "c"] // String 배열
    ```

- **선언과 초기화 분리**
    ```
    var arr: [Double]
    arr = [1.1, 2.2, 3.3]
    ```

- **동적 추가**
    ```
    var arr = [Int]()
    arr.append(10)
    arr += [20,```

- **isEmpty로 비어있는지 확인**
    ```
    if arr.isEmpty {
        print("배열이 비어있다")
    }
    ```

---

## enum을 배열에 넣는 방법

1. **enum 정의 및 배열 선언**
    ```
    enum Direction {
        case north
        case south
        case east
        case west
    }

    var directions: [Direction] = [.north, .south, .east]
    ```

2. **CaseIterable로 모든 case 배열화**
    ```
    enum Direction: CaseIterable {
        case north, south, east, west
    }

    let allDirections = Direction.allCases // [north, south, east, west]
    ```

---

## `var directions: Direction`과 `[Direction]`의 차이

- `var directions: Direction`  
    - Direction 타입의 단일 값만 저장 가능

- `var directions: [Direction]`  
    - 여러 Direction 값을 배열로 저장 가능

    ```
    var direction: Direction = .north // 단일 값
    var directions: [Direction] = [.north, .south] // 여러 값
    ```
