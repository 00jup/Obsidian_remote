
## `is_alive` 사용 이유

`is_alive`는 `match` 문 내의 `case` 패턴에 추가적인 조건, 즉 **가드(guard)** 로 사용됩니다. 

### 기본 구조

```python
match status:
    case 400 if is_alive:

        print("Bad Request")
    
```

### 기능

- `is_alive`의 값이 `True`일 때만 해당 `case` 문이 실행됩니다.
- `status` 값이 400이지만 `is_alive`가 `False`라면 "Bad Request"를 출력하지 않습니다.

### 결과

이러한 가드 조건은 패턴 매칭을 더욱 유연하게 만들어줍니다. 특정 패턴이 일치할 때 추가적인 조건을 검사하여 해당 `case` 문을 실행할지 결정할 수 있습니다.
