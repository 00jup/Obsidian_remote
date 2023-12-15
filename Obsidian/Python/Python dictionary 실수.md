
```python
self.department = {'봉준호': {'개발팀': '대리'},

'박찬욱': {'개발팀': '대리'}, '최동훈': {'서비스팀': '과장'}}
```

위에가 맞음

```python
self.department = {'봉준호': {'개발팀', '대리'},

'박찬욱': {'개발팀', '대리'}, '최동훈': {'서비스팀', '과장'}}
```

갑자기 set 넣는 이상한 짓 하지말기!

## 이것도 set 넣은 거임
```python
from collections import defaultdict


class Company:

    def __init__(self):
        self.people = {}
        self.company_id = 2000

    def come_in(self):
        department = input("부서를 입력하세요: ")
        rank = input("직급을 입력하세요: ")
        name = input("이름을 입력하세요: ")
        if name not in self.people:
            self.people[name] = {}
        self.people[name] = {department, rank, self.company_id}
        print(f"사번은 {company_id}입니다.")
        self.company_id += 1
```

> {department, rank, self.company_id}

그래서 출력하면 순서가 달라져있는 걸 알 수 있음..
