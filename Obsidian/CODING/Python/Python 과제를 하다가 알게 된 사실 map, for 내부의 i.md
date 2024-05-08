
```python
import random

list = []
for i in range(1, 46):
    list.append(i)

random.shuffle(list)

rotto_list = list
print(rotto_list)
input_list = map(int, input("로또 번호를 입력하세요 : ").split())

count = 0
for i in range(0, 6):
    if input_list in rotto_list:
        count += 1

print(rotto_list)
print("당첨 횟수 " + str(count))

```

# map 함수의 사용

map 함수를 살펴보면 다음과 같다.
```
def map(func: Callable[[_T1], _S], iter1: Iterable[_T1], /) -> Iterator[_S]  
def map(func: Callable[[_T1, _T2], _S], iter1: Iterable[_T1], iter2: Iterable[_T2], /) -> Iterator[_S]  
def map(func: Callable[[_T1, _T2, _T3], _S], iter1: Iterable[_T1], iter2: Iterable[_T2], iter3: Iterable[_T3], /) -> Iterator[_S]  
def map(func: Callable[[_T1, _T2, _T3, _T4], _S], iter1: Iterable[_T1], iter2: Iterable[_T2], iter3: Iterable[_T3], iter4: Iterable[_T4], /) -> Iterator[_S]  
def map(func: Callable[[_T1, _T2, _T3, _T4, _T5], _S], iter1: Iterable[_T1], iter2: Iterable[_T2], iter3: Iterable[_T3], iter4: Iterable[_T4], iter5: Iterable[_T5], /) -> Iterator[_S]  
def map(func: Callable[..., _S], iter1: Iterable[Any], iter2: Iterable[Any], iter3: Iterable[Any], iter4: Iterable[Any], iter5: Iterable[Any], iter6: Iterable[Any], /, *iterables: Iterable[Any]) -> Iterator[_S]

---

map(func, *iterables) --> map object
```

평소

> map(int, sys.stdin.readline())

으로 사용했는데, 여기서 int의 경우 자료가 아니라 함수를 의미하는 것이었다.

예를 들어서 A = 4.0일 때 int(A)라는 함수를 쓰면 바뀌는 것처럼 말이다.

# for 내부의 i

for 내부의 i의 경우 무조건 정수를 