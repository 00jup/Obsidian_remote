
```python
import pandas as pd

# 예제 데이터 프레임 생성
df = pd.DataFrame({'A': [1, 2, 3, 4, None],
                   'B': [5, 6, 7, 8, None]})

# isin() 함수 사용
result = df['A'].isin([1, 3])

print(df[result])

print(df[["A", "B"]].dropna())
```

원하는 값이 있다면 True를 return한다.