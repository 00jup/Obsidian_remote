

```python
import pandas as pd
import numpy as np

df = pd.DataFrame(
    {
        "A": ["foo", "bar", "bar", "foo", "bar", "foo"],
        "B": ["one", "one", "two", "two", "one", "three"],
        "C": np.random.random(6),
        "D": np.random.random(6),
    }
)

new = df.groupby(["A", "B"]).sum()
# 모두 다 DataFrame의 형태임

# print(new["A"])
# print(new["B"])
## 출력이 안 되는 이유는 multi index가 되기 때문이다. ##

## 이건 columns에 속하기 때문에 출력이 가능함 ##
print(new["C"])
print(new["D"])

## multi index에 속하기 때문에 아래와 같이 사용가능하다. ##
print(new.loc["bar"])
print(new.loc[("bar", "one")])
print(new.iloc[0])

```

## 사용된 데이터
```python
                  C         D
A   B                        
bar one    0.487843  1.547533
    two    0.530631  0.798497
foo one    0.006691  0.385805
    three  0.318268  0.507702
    two    0.980958  0.585266
```

