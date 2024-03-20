[[Python 수정본]]
[[print(solve(a, b, c))여기서 a,b,c를 입력받음과 동시에 출력하는 방법]]
[[numpy에서의 pythonic]]

# match를 적극 사용하기
```python
is_alive = False
status = 400
match status:
    case 400 if is_alive:
        print("Bad Request")
    case 401 if is_alive:
        print("Unauthorized")
    case 418 | 419 | 420:
        print("I'm a teapot")
    case _:
        print("OK")
```

> 여기서는 is_alive가 flag가 되는 것이다.

# try, exception 같은 느낌
```python
for i in range(5):
    if i>10: 
        print("i>10")
    ###출력될 일 없음 
    ## 한번도 이런 구문이 실행되지 않는다면 이걸 하세요 이렇게 만들 수 있다.
else:
    print("flag is True")
### 만약 이 안에서 흐름을 해치는 구문이 실행되면 이걸 실행해라
### 비밀번호 최대 3번 입력 다 틀리면? 아무것도 못하게 만들어야 하는데 그게 else안에 들어가는 것

```
코드가 정상적으로 5번 실행되었을 때, break 하지 않으면 else로 들어가는 것인가?
[[try except랑 if elif elif else의 차이]]


```python
correct_password = "1234"

for i in range(3):
    input_password = input("비밀번호를 입력하세요: ")
    
    if input_password == correct_password:
        print("비밀번호가 맞았다.")
        break
    else:
        print(f"비밀번호가 틀렸다. {2-i}번의 기회가 남았다.")
else:
    print("비밀번호를 3번 틀렸다. 아무것도 못하게 만든다.")

```


## 변형 1
```python
while (1):
    if numb > 10000:
        numb = int(sys.stdin.readline())
    else:
        break

if numb == 1:
    print("소수입니다.")
else:
    for i in range(2, numb):
        if numb % i is 0:
            print("소수가 아닙니다.")
            break
    else:
        print("소수입니다.")
```

## 변형 2
```python
for divider in range(2, numb):
    if numb % divider == 0:
        print('no')
        break
else:
    print("prime")

```

# 자유로운 for의 사용
```python
i = 0

for i in [0, 1, 2, 3, 4]:
    print(i)

for i in "a b cde":
    print(i)
```

# fibonacci도 이렇게 표현이 가능하다
```python
a, b = 0, 1

while a < 10:
    print(a)
    a, b = b, a+b
```

# print할 때 더 깔끔하게 하기
```python
print(i + " ")

### 이건 아래와 같이 ###

print(i, end=" ")

```


# 변수도 이렇게 한번에 넣을 수 있다.

```python
DEAD = 0
SURVIVED = 1
DEAD, SURVIVED = 0, 1
```

# 배열의 모든 요소를 10으로 초기화하는 방법
```python
size = 10  # 원하는 배열의 크기
array = [10] * size  # 모든 요소를 10으로 초기화
```


[[Python 값을 던지기]]
