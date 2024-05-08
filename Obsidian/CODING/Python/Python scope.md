
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

```

# 출력하면?
다 31이 나온다.