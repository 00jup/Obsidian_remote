네, 주어진 파이썬 코드를 마크다운 형식으로 정리해 드리겠습니다:

---

## 튜플 (Tuple)

### 기본 튜플 선언

```python
a = ()
print(a)
```

### 괄호 없이도 튜플로 인식

```python
a = (1, 2, 3)
a = 1, 2, 3
print(a)
```

### 한 요소만 가진 튜플

괄호 안에 하나의 요소만 있을 경우, 튜플이 아니다. 이를 튜플로 만들기 위해서는 쉼표(,)가 필요하다.

```python
a = (1)
print(a)  # 튜플이 아니다.

a = (1,)
print(a)  # 튜플이다.
```

### 다양한 타입의 요소를 가진 튜플 (Heterogeneous)

```python
a = ("1", 2.1, True)
print(a)

a = tuple(("1", 2.1, True)) #-> 보기 쉽도록 이렇게 작성하기
```

### 중첩 튜플 (Nested Tuple)

```python
a = ((1, 2), (3, 4))
print(a)
print(a[0:100]) # -> 끝까지 나옴
```

### NoneType과 튜플

```python
print(None)       # NoneType
(None, None)      # tuple
(1,)              # 이 경우에 None을 사용하면: 
(1, None)
```

### 튜플의 길이 (Length)

```python
print(len("abc"))
print(len((1, 2,)))
print(len((1, 2, None)))
```

### 튜플에서 요소의 존재 확인

```python
a = ("1", 2.1, True)
print(False in a)
print(2.1 in a)
print(2.2 in a)
```

### 튜플의 연산

```python
b = (1, 2, 2)
print(a + b)  # concatenation
# print(a * b)  # error
print(a * 2

b = (1, 2, 2)
a = (2, 2, 2)
print(a*b) # -> ERROR!
```

### 요소의 인덱스 및 개수 찾기

```python
print(a.index(2.1))
if False in a:
    location = a.index(False)

# 효과적인 방법
location = a.index(True) if True in a else None
print(a.count(False))
```
