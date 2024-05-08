Python에서 `lambda` 함수는 익명 함수(anonymous function)를 정의할 때 사용한다. 기본 함수 정의보다 간결하게 함수를 표현할 수 있다.
[[Python sorted lambda]]

1. **기본 함수 정의:**

```python
def f(a):
    return a + 1
```

2. **`lambda`를 사용한 함수 정의:**

```python
lambda x: x + 1
```

이 `lambda` 함수는 JavaScript의 arrow function과 비슷한 느낌을 가진다. 그렇기 때문에 간단한 로직을 한 줄로 표현하고 싶을 때 유용하다.

3. **`lambda` 함수 사용 예:**

```python
print((lambda a, b: a + b)(10, 20))
```

위 코드는 두 숫자를 더하는 `lambda` 함수를 정의하고, 이를 바로 호출하여 결과를 출력한다. 여기서는 10과 20을 더한 결과인 30이 출력된다.

요약하면, `lambda`는 Python에서 익명 함수를 간결하게 표현할 수 있는 방법이며, 특히 함수를 짧고 간단하게 정의할 때 사용한다.