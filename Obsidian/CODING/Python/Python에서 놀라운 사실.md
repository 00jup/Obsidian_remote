
값을 던질 수 있다는 사실이 정말 놀랍다.

```python
import math


def solve_square_function(a, b, c):
    D = (b ** 2)-(4 * a * c)
    if D >= 0:
        x1 = (-b+math.sqrt(D))/2*a
        x2 = (-b-math.sqrt(D))/2*a
        result = (x1, x2)
    elif D < 0:
        raise Exception("실근 x")

    return result


user_value = list(map(int, input("a, b, c 입력 : ").split(", ")))
# a, b, c = *user_value
# 와 대박이다.
try:
    solve_square_function(*user_value)
except Exception as exp:
    print(type(exp).__name__)
    print("실근이 존재하지 않습니다.")

```

이렇게 값을 던질 수 있다는 사실이 진짜진짜 신기했다.
