python에서 dictionary에 바로 key를 추가하면 key error가 발생한다.
따라서 이걸 해결하려면 아래와 같이 setdefault를 사용하면 된다...


```python
dict = {}
keys = ['a', 'b', 'a', 'c', 'a', 'b']

for key in keys:
    dict.setdefault(key, 0)
    dict[key] += 1

print(dict)  # 출력: {'a': 3, 'b': 2, 'c': 1}
```


