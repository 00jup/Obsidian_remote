[[Python dictionary와 list의 공통점]]
[[Python dictionary indexing in if]]
[[Python dictionary 실수]]
[[Python 시험에서 틀린 것]]
[[Python dictionary 데이터 추가하기]]


dictionary는 set과 마찬가지로 중복을 허용하지 않는다.
그래서 아래와 같은 결과를 얻을 수 있다.
![[Screenshot 2023-10-07 at 16.51.08.png]]

Python의 딕셔너리(dictionary)에서 `items()` 메소드는 딕셔너리의 키-값 쌍들을 튜플로 반환하는 메소드이다.

### 사용 방법:

```python
dictionary.items()
```

### 예시:

```python
dict_example = {'a': 1, 'b': 2, 'c': 3}
print(dict_example.items())  # 결과: dict_items([('a', 1), ('b', 2), ('c', 3)])
```

### 특징:

1. `items()` 메소드의 반환값은 `dict_items` 객체이다. 이 객체는 반복(iterable) 가능하므로 `for` 루프에서 사용할 수 있다.
2. 키-값 쌍들은 튜플로 반환되며, 각 튜플의 첫 번째 요소는 키이고 두 번째 요소는 값이다.

### 활용 예:

딕셔너리의 키와 값을 반복하여 출력하는 경우:

```python
for key, value in dict_example.items():
    print(f"Key: {key}, Value: {value}")
```

이렇게 `items()` 메소드를 사용하면 딕셔너리의 키와 값에 동시에 접근할 수 있어서 매우 유용하다.

[[Python **dic]]
