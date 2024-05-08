
```python
self.department[name]['팀'] = team

self.department[name]['직급'] = rank
```

### 갑자기 이렇게 데이터를 저장하면 안 된다!!

## 1번처럼 하거나
```python
def join(self):
    name = input("이름을 입력하세요: ")
    team = input("부서를 입력하세요: ")
    rank = input("직급을 입력하세요: ")
    company_number = int(input("사번을 입력하세요: "))

    self.people[name] = company_number
    self.department[name] = {'팀': team, '직급': rank}  # 새로운 딕셔너리 항목 생성

```

## 2번처럼 해야 함
```python
def join(self):
    name = input("이름을 입력하세요: ")
    team = input("부서를 입력하세요: ")
    rank = input("직급을 입력하세요: ")
    company_number = int(input("사번을 입력하세요: "))

    self.people[name] = company_number
    if name not in self.department:
        self.department[name] = {}  # name 키에 대한 새로운 딕셔너리를 생성한다.
    self.department[name]['팀'] = team
    self.department[name]['직급'] = rank

```

# 왜냐?
넣을 수 있으려면 self.department[name]에 새로운 딕셔너리로 존재해야 한다.