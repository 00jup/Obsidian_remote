
# 궁금함

```python
a = 1


def f():
    a = 11

    def g():
        nonlocal a
        a = 21

        def r():
            nonlocal a
            a = 31
            print(a)
        r()
        print(f"g : {a}")
    g()
    print(f"f : {a}")


f()
print(f"out : {a}")
```

nonlocal이 외부의 값을 바꿀 수 있을까?

여기서는 out을 제외하고 다 31로 바뀌어서 나온다.

하지만 

## 2
```python
a = 1


def f():
    a = 11

    def g():
        a = 21

        def r():
            nonlocal a
            a = 31
            print(a)
        r()
        print(f"g : {a}")
    g()
    print(f"f : {a}")


f()
print(f"out : {a}")
```

a = 21 위의 nonlocal을 지울 경우
f는 11로 출력되어 나온다.

## 값에 영향을 주는 게 아니라. 주소를 가지고 있으니까 값을 수정할 수 있는 거임.

`nonlocal` 키워드는 현재 함수의 스코프 외부에 있는 가장 가까운 변수를 참조한다. 그래서 첫 번째 코드에서 `r()` 함수의 `nonlocal a`는 `g()` 함수의 `a`를 참조하고, 마찬가지로 `g()` 함수의 `nonlocal a`는 `f()` 함수의 `a`를 참조한다.

`nonlocal` 키워드가 가리키는 변수는 단순히 참조만 하는 것이 아니라, 해당 변수를 직접 수정할 수 있다. 따라서 `r()` 함수에서 `a=31`로 수정하면 `g()` 함수의 `a`가 변경되고, 그 결과 `f()` 함수의 `a` 역시 변경된다.

두 번째 코드에서 `r()` 함수의 `nonlocal a`는 `g()` 함수의 `a`를 참조한다. 여기서도 마찬가지로 `a=31`로 수정하면 `g()` 함수의 `a` 값이 변경된다. 그러나 이 경우에는 `g()` 함수 내부에서 `a`를 새로 선언하고 있으므로, `f()` 함수의 `a`는 영향을 받지 않는다.

즉, `nonlocal`은 현재 스코프에서 가장 가까운 외부 스코프의 변수를 참조하고, 그 변수를 수정할 수 있게 해준다. 따라서 `nonlocal`이 가리키는 변수가 변경되면, 그 변수를 포함하고 있는 함수의 스코프도 영향을 받는다.