이 코드는 이전 코드와 중요한 차이점이 있다. `onChange` 블록 내부에 `if rightTyping` 조건이 추가되었다.

### 차이점 설명

**이전 코드:**

```swift
.onChange(of: leftAmount) {
    rightAmount = leftCurrency.convert(leftAmount, to: rightCurrency)
}
```

**현재 코드:**

```swift
.onChange(of: rightAmount) {
    if rightTyping {
        leftAmount = rightCurrency.convert(rightAmount, to: leftCurrency)
    }
}
```

### 주요 변화:

1. **조건부 변환**:
    
    - 이전: `leftAmount`가 변경될 때마다 항상 `rightAmount`를 업데이트
    - 현재: `rightAmount`가 변경될 때 `rightTyping`이 `true`일 때만 `leftAmount` 업데이트
2. **무한 루프 방지**:
    
    - 이 조건문은 매우 중요하다. `focused`를 사용해 현재 사용자가 실제로 입력 중인 필드를 확인한다.
    - 사용자가 오른쪽 필드에 입력 중일 때만(`rightTyping == true`) 변환을 수행한다.
3. **실용적 이점**:
    
    - 양방향 변환 시 발생할 수 있는 무한 루프 방지
    - 프로그래밍 방식으로 값이 변경될 때는 변환을 건너뛴다
    - 사용자가 실제로 입력하는 필드에 따라 변환 방향 결정

이 접근 방식이 필요한 이유는, 양쪽 필드 모두 `onChange` 이벤트를 가지고 있다면 하나가 업데이트될 때 다른 하나도 업데이트되고, 그 업데이트가 또 다시 첫 번째 필드를 업데이트하는 무한 루프가 발생할 수 있기 때문이다.

`focused`의 역할은 "사용자가 현재 어디에 입력하고 있는지"를 정확히 추적하여 이런 문제를 방지하는 것이다.