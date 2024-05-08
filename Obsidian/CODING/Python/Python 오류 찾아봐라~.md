```python
class CourseManager:
    # def __init__(self, Course):
    #     pass
    def __init__(self, x, y, z):
        self.x, self.y, self.z = x, y, z
        self.average = (self.x.gpa + self.y.gpa + self.z.gpa)/3

    def average(self):
        return self.average

    def search(self, number):
        if self.x.code == number:
            return "{:<4} {:<2} {:<4}".format(self.x.code, self.x.grade, self.x.gpa)
        elif self.y.code == number:
            return "{:<4} {:<2} {:<4}".format(self.y.code, self.y.grade, self.y.gpa)
        elif self.z.code == number:
            return "{:<4} {:<2} {:<4}".format(self.z.code, self.z.grade, self.z.gpa)


manager = CourseManager(a, b, c)
print(manager.average())
print(manager.search(1002))
```







method랑 변수 명이 같으면 안 됨!!