함수에서 `*c`와 `**dic` 형태의 인자를 사용하는 것은 Python에서 가변 인자(variable arguments)와 키워드 가변 인자(keyword variable arguments)를 받기 위한 표기법이다.

1. **`*c` (가변 인자)**
   - 함수를 정의할 때 `*c` 형식의 인자를 사용하면, 그 함수는 위치 기반의 가변 수의 인자를 받을 수 있다.
   - 이러한 인자들은 함수 내부에서 튜플(tuple) 형태로 표현된다.
   
   예시:
   ```python
   def func(*args):
       for arg in args:
           print(arg)
   
   func(1, 2, 3, 4)  # 출력: 1 2 3 4
   ```

2. **`**dic` (키워드 가변 인자)**
   - 함수를 정의할 때 `**dic` 형식의 인자를 사용하면, 그 함수는 키워드 기반의 가변 수의 인자를 받을 수 있다.
   - 이러한 인자들은 함수 내부에서 사전(dictionary) 형태로 표현된다.
   
   예시:
   ```python
   def func(**kwargs):
       for key, value in kwargs.items():
           print(f"{key} = {value}")
   
   func(a=1, b=2, c=3)  # 출력: a = 1, b = 2, c = 3
   ```

이러한 표기법의 이점:
- 함수에 전달되는 인자의 수가 미리 정해지지 않았을 때 유용하다. 예를 들어, 리스트나 튜플, 사전의 요소들을 함수의 인자로 펼쳐서 전달하고 싶을 때 사용한다.
- API나 라이브러리 함수를 설계할 때, 사용자가 다양한 방식으로 함수를 사용할 수 있도록 유연성을 제공한다.
- 기존의 함수 시그니처를 변경하지 않고 새로운 인자를 추가할 수 있다. 이는 특히 라이브러리나 프레임워크에서 중요한데, 기존 사용자의 코드를 깨뜨리지 않으면서 새로운 기능을 추가할 수 있다.