
```python
for i in range(5):
     for j in range(5):
         sum_data[i, j] = new_data[i, j] + new_data[i+1, j+1] + \
             new_data[i+1, j] + new_data[i, j+1]


for i in range(5):
    for j in range(5):
        sum_data[i, j] = data[2*i:2*i+1, 2*j:2*j+1].sum(axis=1)
        sum_data[i, j] = data[2*i:2*i+1, 2*j:2*j+1].sum(axis=0)
```


첫번째가 C스러운 코드이고

그 다음이 pythonic 답다고 할 수 있지 않겠느냐.
