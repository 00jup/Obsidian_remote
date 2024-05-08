```python
import math


def f(a, b, c, g): return a*(g**2) + b * g + c


def g(a, b, c, x): return a*math.sin(b*x)+c


values = input().split()

for i in range(len(values)):
    values[i] = float(values[i])

print(f(*values[:3], g(*values)))
```

가변 인자를 던지는 거임