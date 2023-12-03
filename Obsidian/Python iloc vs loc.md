
```python
import numpy as np
import pandas as pd

df = pd.DataFrame(np.random.random((5,5)), columns = ['a','b','c','d','e'])

print(df.loc[:,'a'])
print(df.iloc[:,1])
```

iloc의 i는 index를 의미한다.

따라서 위에서 loc과 다르게 1로 index를 표시해줘야 출력할 수 있다.
