
## class 변수를 사용하는 법은 2가지인가?
```python
class Myclass:
    money = 1000

    def __init__(self):
        self.money = 2000

    @classmethod
    def class_method1(cls):
        cls.money = 3000

    def class_method2(self):
        Myclass.money = 4000

    def __repr__(self):
        return str(f"{self.money}, {Myclass.money}")


person = Myclass()
person.class_method1()
print(person)

person.class_method2()
print(person)
```


[[Python repr, str 표현자]]
[[Python에서 imagine number operation]]
