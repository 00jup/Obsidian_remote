
```python
# a[11::12] 12월 데이터만
# ㅗㅜㅑ Holy shit!!!!!!!!!!
# a[::2] 짝수 indexing
# a[1::2] 홀수 indexing
# a[11::12] 12월 데이터만
# a[::-2] 짝수 indexing 역순
```

아래는 전문임
```python
a = []
print(a)

a = [1, 2, 3]
print(a)
a = list([1, 2, 3])
print(a)
a = [1, 2, 3, [4, 5]]
print(a)
print(a[3][1])

# 상자에는 이걸 하나만 담기 위해 존재함
# 리스트는 하나만 있어도 자료 구조로 기능할 수 있다. 그래서 본질적으로 차이나는 것
# a = (1) 랑 a = [1]은 다르다.

a = list((1, 2, 3))
print(a)
a = tuple([1, 2, 3])
print(a)

a = [(1, 2), (3, 4)]
print(a)
a = [[1, 2], [3, 4]]
print(a)
print(a * 2)

a = ["1"]
a.append(100)
print(a)

a.extend([200, 300])
print(a)
# 위 아래는 다르다. extend 공간을 확장 append는 안에 집어 넣는다.
a.append([200, 300])
print(a)

a.insert(0, 0)
print(a)

a.remove(0)
print(a)

b = a.pop()
print(a)

a.clear()
print(a)

# 어떤 값이 들어가는지 코드만 보고 짐작해야 한다.

a = ['1', 1, 10, True, '1']
# heterogeneous data
a.remove('1')
# 처음이 지워진다고 정해진 것임.

# 정렬은 컴퓨터공학도면 알아야 한다. 안 짜도 되지만 지금 짜라고 해도 짤 수 있을 정도로..
# 정렬은 무조건 알아야 한다.
# 정렬은 비용이 많아서 항상 정렬을 하려고 하면 안 된다.
# python에서는 team sort를 쓴다.

# a.sort()
# a라는 나열에 대해서 sort 원본 데이터가 변함
# sorted(a)
# sorting이 목적이고 거기에 나열 하나를 넣은 것임. 원본 데이터는 변하지 않음
# ->-> 파이썬의 중요한 철학 orgin 데이터를 변환시키지 않는다.
# 기능의 실행결과가 반환된다면 orign 변화시키지 않는다. 반환하지 않는다면 orgin 변화시킨다.
# library
# a.reverse()
# reversed(a)도 있음. 나열이 튜플일지 리스트일지 모르니까 list(reversed(a)) 이렇게 써야 함.

# print(a[::-1]) 이것도 가능함. range(b,e,s) 1 , 10 , 2 2씩 증가하면서 빼라
# 여기서도 slicing을 확장 [0:2:1] , [0:10:2] -> [0,2,4,6,8]

# ㅗㅜㅑ Holy shit!!!!!!!!!!
# a[::2] 짝수 indexing
# a[1::2] 홀수 indexing
# a[11::12] 12월 데이터만
# a[::-2] 짝수 indexing 역순

# print(a.copy()) 복사하는 기능도 있음 15주차 때 말할 것
a = '1,2,3,4,5'
tokens = a.split(',')
print(tokens)
# c에서는 strtok 이라는 함수가 있음
# split으로 다 끝낸다. 뭘 대상으로 자를지 delimitor를 집어넣어준다.
a = '1 2 3 4 5'
tokens = a.split(' ')
print(tokens)

a = 'yesterday is today'
token1, token2, token3 = a.split()
print(token1)
print(token2)
print(token3)
# txt를 이렇게 읽을 수 있다.


ㅁ = ("1", 2.1, True)
print(ㅁ[-3])
print(ㅁ[-2])
print(ㅁ[-1])
print(ㅁ[-1])

```