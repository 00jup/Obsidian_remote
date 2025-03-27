
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