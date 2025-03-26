Swift의 `switch` 문에서는 일반적으로 모든 가능한 케이스를 처리해야 합니다. 이것은 "완전한 스위치(exhaustive switch)"라고 불립니다.

다음과 같은 경우에 `default` 케이스가 필요합니다:

1. **열거형(enum)이 아닌 타입을 사용할 때**:
    
    ```swift
    let number = 5
    switch number {
        case 1: print("One")
        case 2: print("Two")
        // 모든 정수 값을 개별적으로 처리할 수 없으므로 default 필요
        default: print("Other number")
    }
    ```
    
2. **불완전한 열거형을 사용할 때**:
    
    ```swift
    enum Direction {
        case north, south, east, west
        case northeast, northwest, southeast, southwest
    }
    
    let direction = Direction.north
    switch direction {
        case .north: print("Going north")
        case .south: print("Going south")
        // 모든 케이스를 명시적으로 처리하지 않았으므로 default 필요
        default: print("Going somewhere else")
    }
    ```
    

그러나 다음과 같은 경우에는 `default`가 필요하지 않습니다:

1. **모든 케이스를 명시적으로 다룰 때**:
    
    ```swift
    enum TrafficLight {
        case red, yellow, green
    }
    
    let light = TrafficLight.red
    switch light {
        case .red: print("Stop")
        case .yellow: print("Caution")
        case .green: print("Go")
        // 모든 가능한 케이스를 처리했으므로 default 불필요
    }
    ```
    
2. **@unknown default를 사용하는 경우**:
    
    ```swift
    enum APIStatus {
        case success, failure, pending
    }
    
    let status = APIStatus.success
    switch status {
        case .success: print("API call succeeded")
        case .failure: print("API call failed")
        case .pending: print("API call is pending")
        @unknown default: print("Unknown status")
        // 현재는 모든 케이스를 처리했지만, 미래에 enum에 케이스가 추가될 경우 대비
    }
    ```
    

따라서 Swift에서는 모든 가능한 케이스를 명시적으로 처리하지 않는 한 `default` 케이스가 필요합니다. 이는 코드의 안전성을 높이는 Swift의 중요한 설계 원칙입니다.