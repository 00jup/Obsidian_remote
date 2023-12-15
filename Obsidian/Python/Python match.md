물론입니다. Python 3.10부터 도입된 `match`-`case` 문에 대한 내용을 마크다운 형식으로 정리하겠습니다.

---

# Python 3.10의 `match`-`case` 문

Python 3.10 이상에서 사용할 수 있는 `match`-`case` 문은 다양한 데이터 타입과 패턴을 지원합니다. 이는 일반적인 `if`-`elif`-`else` 구문보다 훨씬 강력하고 가독성 있는 코드를 작성할 수 있게 해줍니다.

## 기본 사용법

`match` 문을 사용하여 값을 매칭하고, `case` 문을 이용해 매칭되는 값을 처리합니다.

```python
match expression:
    case pattern1:
        # do something
    case pattern2:
        # do something else
    case _:
        # default case
```

## 문자열과 소수점 패턴

문자열이나 소수점(float) 등도 매칭할 수 있습니다.

### 문자열 패턴 예시
```python
def greet(language):
    match language:
        case "English":
            return "Hello"
        case "Spanish":
            return "Hola"
        case "French":
            return "Bonjour"
        case _:
            return "Unknown language"
```

### 소수점 패턴 예시
```python
def classify_number(num):
    match num:
        case 0.0:
            return "Zero"
        case 1.0:
            return "One"
        case _:
            return "Other"
```

## 변수를 사용하는 경우

변수는 패턴 매칭에서 '와일드카드'처럼 작동하여 어떤 값이든 매칭될 수 있습니다.

### 변수 사용 예시
```python
def describe(value):
    match value:
        case 0:
            return "zero"
        case 1:
            return "one"
        case int(n):
            return f"an integer greater than one, got {n}"
        case float(n):
            return f"a float, got {n}"
        case str(s):
            return f"a string, got {s}"
        case _:
            return "something else"
```

### 와일드카드 변수
와일드카드 변수는 어떠한 값도 받을 수 있습니다.

```python
def echo(value):
    match value:
        case 0:
            return "zero"
        case 1:
            return "one"
        case x:
            return f"Received: {x}"
```

`case x:`는 어떠한 값이든 `x`에 할당하고, 해당 `case` 블록 내에서 그 값을 사용할 수 있습니다.


### 사용 예시
```python
while (True):
    control = int(input("작업을 선택하세요."))
    match control:
        case 1 | 2:
            pass
        case 3:
            pass
        case 4:
            pass
        case 5:
            break
        case _:
            print("잘못 입력하셨습니다.")
```
