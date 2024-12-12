

```python
# Numpy array의 경우
import numpy as np
a = np.array([[1,2], [3,4]])
b = a.copy()  # 완전한 deep copy가 된다
a[0][0] = 99
print("Numpy copy 후:")
print("a:", a)        # [[99, 2], [3, 4]]
print("b:", b)        # [[1, 2], [3, 4]]  # 영향 없음

# List의 경우
original = [[1,2], [3,4]]
shallow = original.copy()  # shallow copy만 된다
original[0][0] = 99
print("\nList copy 후:")
print("original:", original)  # [[99, 2], [3, 4]]
print("shallow:", shallow)    # [[99, 2], [3, 4]]  # 영향 받음
```

numpy의 copy()는 기본적으로 deep copy로 동작하지만, 파이썬 리스트의 copy()는 shallow copy로 동작한다. 이는 numpy가 과학 계산용으로 설계되어 데이터 무결성을 더 중요하게 고려했기 때문이다.