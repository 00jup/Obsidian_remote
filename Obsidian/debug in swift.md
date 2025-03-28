Swift에서 함수 내부를 디버깅하는 방법들을 알려드리겠다:

1. `print()` 문 사용:

```swift
func calculate(a: Int, b: Int) -> Int {
    print("함수 시작: a=\(a), b=\(b)")
    let result = a * b + a
    print("계산 결과: \(result)")
    return result
}
```

2. `debugPrint()` 사용 (더 상세한 정보):

```swift
func process(data: [String: Any]) {
    debugPrint("처리할 데이터:", data)
    // 처리 로직...
}
```

3. `assert()` 사용 (디버그 모드에서만 작동):

```swift
func divide(a: Double, b: Double) -> Double {
    assert(b != 0, "0으로 나눌 수 없습니다!")
    return a / b
}
```

4. Xcode 중단점(breakpoint) 설정:
    
    - 코드 라인 번호 옆을 클릭하여 중단점 설정
    - 중단점에서 변수 검사, 단계별 실행 가능
5. `#file`, `#line`, `#function` 등의 리터럴 사용:
    

```swift
func complexOperation() {
    print("현재 파일: \(#file), 함수: \(#function), 라인: \(#line)")
    // 로직...
}
```

6. 조건부 중단점 설정:
    
    - Xcode에서 중단점 우클릭 > 편집
    - 조건 추가 (예: `count > 100`)
7. LLDB 디버거 명령어 사용:
    
    - `po` (print object): `po someVariable`
    - `p` (print): `p someVariable`
    - `bt` (backtrace): 호출 스택 확인
8. `dump()` 함수 사용 (객체의 자세한 구조 출력):
    

```swift
func analyze(object: Any) {
    dump(object)
    // 분석 로직...
}
```

9. 로깅 프레임워크 사용 (OSLog, SwiftyBeaver 등)
    
10. 심볼릭 브레이크포인트 설정 (특정 메서드가 호출될 때):
    
    - Xcode > Debug > Breakpoints > Create Symbolic Breakpoint