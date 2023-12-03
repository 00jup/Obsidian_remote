`__repr__`과 `__str__`는 둘 다 Python 클래스 내에서 객체를 문자열로 표현하는 매직 메소드이다. 그러나 사용되는 상황과 목적이 다르다.

1. `__repr__`:
   - 객체의 "공식적인" 문자열 표현을 제공한다. 주로 개발자에게 객체를 나타내는 명확하고, 식별 가능한 문자열 표현을 제공하기 위해 사용된다.
   - 대화식 인터프리터에서 객체 이름을 입력하고 실행할 때 호출된다.
   - `repr()` 내장 함수로 호출될 때 사용된다.
   - `__str__`이 구현되어 있지 않을 경우, `str()`과 `print()` 함수에서 객체를 문자열로 변환할 때 `__repr__`이 호출된다.

2. `__str__`:
   - 객체의 "비공식적인" 또는 "사용자 친화적인" 문자열 표현을 제공한다.
   - 사용자가 객체에 대한 정보를 보기 쉬운 형식으로 보려고 할 때 유용하다.
   - `str()` 내장 함수로 호출될 때 사용된다.
   - `print()` 함수에서 객체를 출력할 때 호출된다.

간단한 예시:

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def __repr__(self):
        return f"Person('{self.name}', {self.age})"
    
    def __str__(self):
        return f"{self.name}, {self.age} years old"

person = Person("John", 30)
print(repr(person))  # 출력: Person('John', 30)
print(str(person))   # 출력: John, 30 years old
print(person)        # 출력: John, 30 years old (여기서는 __str__이 호출됨)
```

이 예시에서, `__repr__` 메소드는 객체의 공식적인 표현을 제공하며, `__str__` 메소드는 더 사람 친화적인 형식의 표현을 제공한다.


교수님은 `__repr__`을 좋아함.