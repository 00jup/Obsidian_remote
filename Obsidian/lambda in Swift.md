
```swift
// 일반적인 함수
func add(a: Int, b: Int) -> Int {
    return a + b
}

// 동일한 기능의 클로저
let addClosure = { (a: Int, b: Int) -> Int in
    return a + b
}

// 사용 방법
add(a: 5, b: 3)      // 8
addClosure(5, 3)     // 8
```

Swift에서 클로저(익명 함수)의 사용법을 설명한다:

## 기본 문법과 사용법

1. **기본 형태**:
    
    ```swift
    { (매개변수) -> 반환타입 in
        // 코드
        return 결과값
    }
    ```
    
2. **변수에 저장하여 사용**:
    
    ```swift
    let multiply = { (x: Int, y: Int) -> Int in
        return x * y
    }
    
    let result = multiply(4, 5) // 20
    ```
    
3. **타입 추론 사용**:
    
    ```swift
    // 타입 추론으로 반환 타입 생략
    let add = { (a: Int, b: Int) in
        return a + b
    }
    ```
    
4. **축약 문법**:
    
    ```swift
    // 단일 표현식일 때 return 생략
    let subtract = { (a: Int, b: Int) in a - b }
    
    // 매개변수 이름 대신 $0, $1 등 사용
    let square = { $0 * $0 }
    let sum = { $0 + $1 }
    ```
    

## 함수에 클로저 전달하기

1. **함수 매개변수로 클로저 전달**:
    
    ```swift
    func calculate(a: Int, b: Int, operation: (Int, Int) -> Int) -> Int {
        return operation(a, b)
    }
    
    // 호출
    let result = calculate(a: 10, b: 5, operation: { $0 + $1 })
    ```
    
2. **후행 클로저 문법**:
    
    ```swift
    // 마지막 매개변수가 클로저일 때 더 깔끔한 문법
    let result = calculate(a: 10, b: 5) { $0 + $1 }
    ```
    

## 실제 활용 예시

1. **배열 고차 함수에서 사용**:
    
    ```swift
    let numbers = [1, 2, 3, 4, 5]
    
    // map: 각 요소를 변환
    let doubled = numbers.map { $0 * 2 } // [2, 4, 6, 8, 10]
    
    // filter: 조건에 맞는 요소만 선택
    let evenNumbers = numbers.filter { $0 % 2 == 0 } // [2, 4]
    
    // reduce: 요소들을 결합
    let sum = numbers.reduce(0) { $0 + $1 } // 15
    ```
    
2. **비동기 작업에서 사용**:
    
    ```swift
    func fetchData(completion: (Data?) -> Void) {
        // 데이터 가져오는 비동기 작업 후
        completion(someData)
    }
    
    // 호출
    fetchData { data in
        if let data = data {
            // 데이터 처리
        }
    }
    ```
    
3. **정렬에 사용**:
    
    ```swift
    let names = ["Tim", "Bob", "Anna", "Zach"]
    let sortedNames = names.sorted { $0 < $1 } // 오름차순
    ```
    

이러한 방식으로 Swift에서 클로저를 코드를 더 간결하고 표현력 있게 만들 수 있다.