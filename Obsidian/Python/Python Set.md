
```python
value_list = list('111234')

print(value_list[:2])
print(value_list[2:])
print(set(value_list[:2]) < set(value_list[2:]))
value_list = list('121134')

print(set(value_list[:2]) < set(value_list[2:]))
print(set(value_list[:2]) ^ set(value_list[2:]))

```

python에서 set의 의미를 바로 알 수 있는 예제이다.

python에서 set은 일단 중복을 허용하지 않는다.

그래서  ``set([1, 1])`` 은 {1}이 된다.