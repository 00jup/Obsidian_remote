
```python
import pandas as pd
import numpy as np

df = pd.DataFrame(np.random.random((3,3)), columns=["a","b","c"])

for column in df:
	print(column)
	print(df[column])

for index in range(df.shape[1]):
	column = df.column[index]
	print(df[column])

for index, serise in df.itemrows():
	print(index)
	print()
	
```


	column = df.column[index] -> df.columns임!!!!

위에서 df에 columns에 `["a","b","c"]` 를 넣었으니까
