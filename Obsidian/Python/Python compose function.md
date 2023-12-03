# 수정 전
```python
a = 1


def f():
    def g():
        def r():
            print(a)


f(g(r()))
```

# 수정 후
```python
a = 1


def f():
    def g():
        def r():
            print(a)
        r()
    g()


f()
```

## 만약 f(g(r())) 이렇게 쓰고 싶다면?

함수를 분리해야 한다.
```python
def f(val):
    print("f:", val)

def g(val):
    print("g:", val)
    return "value from g"

def r():
    print("r")
    return "value from r"

f(g(r()))
```

[[유효범위 문제]]

[[nonlocal은 외부에도 영향을 줄 수 있는가?]]
