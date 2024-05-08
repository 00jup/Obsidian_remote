

```python
import numpy as np
import pandas as pd

filename = "titanic.csv"
data = pd.read_csv(filename)
data = data[["Age", "Fare", "Survived"]].dropna()
data["Age-band"] = np.floor(data["Age"]/10)*10
# NaN 있으면 계산 안 됨

```

Age-band를 만들기 전에 NaN를 없애 줘야 함.

```
      Age
0    22.0
1    38.0
2    26.0
3    35.0
4    35.0
..    ...
886  27.0
887  19.0
888   NaN
889  26.0
890  32.0

[891 rows x 1 columns]
```

888과 같은 data

# 잘못 이해하고 있었음

```python
import numpy as np
import pandas as pd

filename = "titanic.csv"
data = pd.read_csv(filename)

data["Age-band"] = np.floor(data["Age"]/10)*10


data = data[["Age-band", "Fare", "Survived"]].dropna()
data = data.astype({"Age-band": int})

data = data.groupby(["Survived", "Age-band"]).mean()
# 순서 맞춰서 적는 습관가지기

# version1
new_data = pd.DataFrame(index=[0, 10, 20, 30, 40, 50, 60, 70, 80],
                        columns=["Dead", "Survived"])

new_data['Dead'] = data.loc[0]
new_data['Survived'] = data.loc[1]


new_data.to_csv("result.csv")

read = pd.read_csv("result.csv")

print(read)
```
위 코드에서

```python
data = data.astype({"Age-band": int})

```

이렇게 사용해서 에러가 나왔던 것임