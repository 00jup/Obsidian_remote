```python
a = [(1, 2, 1), (0, 1, 3), (5, 1, 4), (5, 2, 0), (3, 0, 1)]

b = sorted(a)
print(b)

c = sorted(a, key=lambda x: x[0])
print(c)

d = sorted(a, key=lambda x: x[1])
print(d)

d = sorted(a, key=lambda x: x[2])
print(d)

```

# 이게 진짜 신기하다

lambda를 기준으로 정렬한다는 거
