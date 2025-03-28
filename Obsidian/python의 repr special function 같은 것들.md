물론 클래스에서도 가능하다. 클래스에서 `CustomStringConvertible`과 `CustomDebugStringConvertible` 프로토콜을 구현하는 예제를 보여주겠다:

```swift
class Person: CustomStringConvertible, CustomDebugStringConvertible {
    var name: String
    var age: Int
    
    init(name: String, age: Int) {
        self.name = name
        self.age = age
    }
    
    // 일반 출력용 (print() 사용 시)
    var description: String {
        return "\(name), \(age)세"
    }
    
    // 디버깅용 출력 (debugPrint() 사용 시)
    var debugDescription: String {
        return "Person(name: \"\(name)\", age: \(age))"
    }
}

let person = Person(name: "김철수", age: 30)
print(person) // "김철수, 30세" 출력
debugPrint(person) // "Person(name: "김철수", age: 30)" 출력
```

클래스는 구조체와 마찬가지로 이러한 프로토콜들을 동일하게 구현할 수 있다. 이 프로토콜들은 타입에 관계없이 사용 가능하다.

아름답다.

