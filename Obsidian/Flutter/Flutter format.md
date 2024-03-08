# Python의 `format` 메서드 사용법

Python의 `format` 메서드는 문자열 내에 특정 값을 삽입하고, 그 형식을 지정할 때 사용된다.

## 기본 사용법

- 중괄호 `{}`를 사용하여 문자열 내에서 대체될 위치를 지정한다.

```python
"Hello, {}!".format("world")
```

- 위치 지정자를 사용하여 인자들의 순서를 지정할 수 있다.

```python
"{1} is {0} years old.".format(30, "Alice")
```

## 서식 지정자를 사용한 고급 사용법

- 정렬과 너비 지정, 숫자 형식 지정 등 세밀한 조정이 가능하다.

### 문자열 정렬

```python
# 왼쪽 정렬
"{:<10}".format("left")

# 가운데 정렬
"{:^10}".format("center")

# 오른쪽 정렬
"{:>10}".format("right")
```

### 숫자 서식 지정

```python
# 소수점 아래 두 자리로 제한
"{:.2f}".format(3.141592)

# 천 단위 구분 기호 추가
"{:,}".format(1000000)
```

### 진법 변환

```python
# 16진수
"{:x}".format(255)

# 8진수
"{:o}".format(255)

# 2진수
"{:b}".format(255)
```

### 날짜 및 시간 서식 지정

```python
from datetime import datetime
now = datetime.now()
"{:%Y-%m-%d %H:%M}".format(now)
```

이와 같이 `format` 메서드는 문자열 포매팅을 위해 다양하게 활용될 수 있다.
```