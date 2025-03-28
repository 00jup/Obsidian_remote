## Value Types (값 타입)

값 타입은 변수나 상수에 할당될 때, 또는 함수에 전달될 때 **값이 복사**됩니다. Swift에서 값 타입으로 분류되는 것들:

- 구조체(Struct)
- 열거형(Enum)
- 튜플(Tuple)
- 기본 데이터 타입(Int, Double, String, Bool 등)

### 예시 1: 기본 데이터 타입

```swift
// Int는 값 타입
var a = 10
var b = a  // a의 값이 b로 복사됨
b = 20     // b만 변경됨

print("a: \(a)")  // a: 10 (원본 값은 변경되지 않음)
print("b: \(b)")  // b: 20
```

### 예시 2: 구조체

```swift
struct Point {
    var x: Int
    var y: Int
}

var point1 = Point(x: 5, y: 10)
var point2 = point1  // point1의 값이 point2로 복사됨
point2.x = 15        // point2만 변경됨

print("point1: \(point1.x), \(point1.y)")  // point1: 5, 10 (원본 유지)
print("point2: \(point2.x), \(point2.y)")  // point2: 15, 10
```

### 예시 3: 함수에 값 타입 전달

```swift
struct Size {
    var width: Double
    var height: Double
}

func modifySize(_ size: Size) -> Size {
    var newSize = size  // 값이 복사됨
    newSize.width *= 2
    newSize.height *= 2
    return newSize
}

let originalSize = Size(width: 10.0, height: 20.0)
let modifiedSize = modifySize(originalSize)

print("Original: \(originalSize.width) x \(originalSize.height)")  // Original: 10.0 x 20.0
print("Modified: \(modifiedSize.width) x \(modifiedSize.height)")  // Modified: 20.0 x 40.0
```

### 예시 4: 배열의 복사 (Array는 값 타입)

```swift
var array1 = [1, 2, 3]
var array2 = array1  // 배열이 복사됨
array2.append(4)     // array2만 변경됨

print("array1: \(array1)")  // array1: [1, 2, 3]
print("array2: \(array2)")  // array2: [1, 2, 3, 4]
```

### 예시 5: 딕셔너리의 복사 (Dictionary도 값 타입)

```swift
var dict1 = ["a": 1, "b": 2]
var dict2 = dict1  // 딕셔너리가 복사됨
dict2["c"] = 3     // dict2만 변경됨

print("dict1: \(dict1)")  // dict1: ["a": 1, "b": 2]
print("dict2: \(dict2)")  // dict2: ["a": 1, "b": 2, "c": 3]
```

## Reference Types (참조 타입)

참조 타입은 변수나 상수에 할당될 때, 또는 함수에 전달될 때 **값이 복사되지 않고 참조(메모리 주소)가 전달**됩니다. Swift에서 참조 타입으로 분류되는 것들:

- 클래스(Class)
- 클로저(Closure)

### 예시 1: 기본 클래스

```swift
class Person {
    var name: String
    
    init(name: String) {
        self.name = name
    }
}

let person1 = Person(name: "Anna")
let person2 = person1  // person1의 참조가 person2로 복사됨
person2.name = "Bob"   // 공유된 인스턴스가 변경됨

print("person1.name: \(person1.name)")  // person1.name: Bob (원본도 변경됨)
print("person2.name: \(person2.name)")  // person2.name: Bob
```

### 예시 2: 복잡한 클래스

```swift
class Car {
    var brand: String
    var model: String
    var year: Int
    
    init(brand: String, model: String, year: Int) {
        self.brand = brand
        self.model = model
        self.year = year
    }
    
    func description() -> String {
        return "\(year) \(brand) \(model)"
    }
}

let car1 = Car(brand: "Toyota", model: "Corolla", year: 2020)
let car2 = car1  // 참조가 복사됨
car2.year = 2022  // 공유된 인스턴스가 변경됨

print("car1: \(car1.description())")  // car1: 2022 Toyota Corolla (원본도 변경됨)
print("car2: \(car2.description())")  // car2: 2022 Toyota Corolla
```

### 예시 3: 함수에 참조 타입 전달

```swift
class Counter {
    var count: Int = 0
}

func incrementCounter(_ counter: Counter) {
    counter.count += 1  // 원본 객체가 변경됨
}

let myCounter = Counter()
print("Before: \(myCounter.count)")  // Before: 0

incrementCounter(myCounter)
print("After: \(myCounter.count)")   // After: 1
```

### 예시 4: 배열 내의 참조 타입

```swift
class Task {
    var name: String
    var isCompleted: Bool = false
    
    init(name: String) {
        self.name = name
    }
}

// 태스크 배열 생성
let task1 = Task(name: "Study Swift")
let task2 = Task(name: "Exercise")
var tasks = [task1, task2]

// 배열의 첫 번째 태스크를 완료로 표시
tasks[0].isCompleted = true

print("task1.isCompleted: \(task1.isCompleted)")  // task1.isCompleted: true
```

### 예시 5: 클래스 내의 클래스 속성

```swift
class Department {
    var name: String
    
    init(name: String) {
        self.name = name
    }
}

class Employee {
    var name: String
    var department: Department
    
    init(name: String, department: Department) {
        self.name = name
        self.department = department
    }
}

let engineering = Department(name: "Engineering")
let john = Employee(name: "John", department: engineering)
let jane = Employee(name: "Jane", department: engineering)

// 부서 이름 변경
engineering.name = "Software Engineering"

print("John's department: \(john.department.name)")  // John's department: Software Engineering
print("Jane's department: \(jane.department.name)")  // Jane's department: Software Engineering
```

## 값 타입과 참조 타입의 식별

참조 타입은 동일성 연산자(`===`)를 사용하여 두 변수가 같은 인스턴스를 참조하는지 확인할 수 있습니다:

```swift
class Student {
    var name: String
    
    init(name: String) {
        self.name = name
    }
}

let student1 = Student(name: "Min")
let student2 = student1
let student3 = Student(name: "Min")

print(student1 === student2)  // true (같은 인스턴스 참조)
print(student1 === student3)  // false (다른 인스턴스)
```

## 값 타입과 참조 타입의 성능 특성

### 값 타입

- 스택 메모리에 저장되는 경향이 있음
- 작은 데이터에 효율적
- 복사 비용이 발생하지만, 최적화를 통해 실제 변경이 있을 때만 복사(copy-on-write)
- 스레드 안전성이 더 높음 (각 스레드가 자체 복사본을 가짐)

### 참조 타입

- 힙 메모리에 저장됨
- 큰 데이터 구조에 효율적 (복사 비용 없음)
- 참조 카운팅과 메모리 관리가 필요함
- 여러 참조가 같은 인스턴스를 가리킬 수 있어 의도하지 않은 변경 가능성

## 언제 무엇을 사용해야 할까?

### 값 타입(Struct)을 사용하는 경우:

- 단순한 데이터 값을 표현할 때
- 복사될 때 독립적인 상태를 유지해야 할 때
- 다른 타입에 내장될 때 참조보다 값으로 전달되어야 할 때
- 스레드 간 데이터 공유가 필요할 때 안전성이 중요할 때

### 참조 타입(Class)을 사용하는 경우:

- 공유된 상태를 모델링할 때
- 객체의 수명 주기나 식별성이 중요할 때
- 상속이 필요할 때
- 인스턴스가 파괴되기 전에 할당된 리소스를 해제해야 할 때 (deinit 사용)