네, 주어진 파이썬 코드를 마크다운 형식으로 정리해 드리겠습니다:

---
> append나 extend, insert의 경우 list에서만 가능하다.
## 리스트 (List)

### 기본 리스트 선언

```python
a = []
print(a)

a = [1, 2, 3]
print(a)
```

### 리스트와 튜플 간의 변환

```python
a = list((1, 2, 3))
print(a)
a = tuple([1, 2, 3])
print(a)
```

### 중첩 리스트

```python
a = [1, 2, 3, [4, 5]]
print(a)
print(a[3][1]) # -> 4
```

### 리스트의 연산

```python
a = [[1, 2], [3, 4]]
print(a)
print(a * 2)
```

### 리스트의 요소 추가 append와 extend는 차이가 있음

```python
a = ["1"]
a.append(100)
print(a)

a.extend([200, 300])
print(a)
# -> [100, 200, 300]

# 위 아래는 다르다. extend 공간을 확장 append는 안에 집어 넣는다.
a.append([200, 300])
# -> [100, [200, 300]]
a.append((200, 300))
# -> [100, (200, 300)]
print(a)
# tuple을 넣는 것도 가능하다.


```

```python
a.append(500, 600)
```
-> 오류남

### 리스트 요소의 삽입과 제거

```python
a.insert(0, 0)
print(a)

a.remove(0)
print(a)

b = a.pop()
print(a)

a.clear()
print(a)
```
[[Python 리스트 찾기 slicing]]

### 리스트 정렬과 역순

Note: 파이썬에서는 원본 데이터를 변환시키지 않는 것이 중요한 철학 중 하나입니다. 

```python
# a.sort()  # 원본 데이터를 변환
# sorted(a) # 원본 데이터를 변환시키지 않음

# a.reverse() # 원본 데이터를 변환
# list(reversed(a)) # 원본 데이터를 변환시키지 않음
```

### 리스트 슬라이싱

```python
# print(a[::-1])   # 전체 리스트 역순
# a[::2]           # 짝수 인덱싱
# a[1::2]          # 홀수 인덱싱
# a[::-2]          # 짝수 인덱싱 역순
```

### 문자열 분리

```python
a = '1,2,3,4,5'
tokens = a.split(',')
print(tokens)

a = '1 2 3 4 5'
tokens = a.split(' ')
print(tokens)

a = 'yesterday is today'
token1, token2, token3 = a.split()
print(token1, token2, token3)
# c에서의 strtok가 이렇게 나타난다.
```

### 음수 인덱스

```python
ㅁ = ("1", 2.1, True)
print(ㅁ[-3])
print(ㅁ[-2])
print(ㅁ[-1])
`