# defaultdict
```python
# Default factory function is list
dd_list = defaultdict(list)
dd_list['key1'].append(1)
print(dd_list)

# Default factory function is int
dd_int = defaultdict(int)
dd_int['key1'] += 1
print(dd_int)

# Default factory function is set
dd_set = defaultdict(set)
dd_set['key1'].add(1)
print(dd_set)

# Default factory function is dict
dd_dict = defaultdict(dict)
dd_dict['key1']['inner_key1'] = 1
print(dd_dict)

# Default factory function is str
dd_str = defaultdict(str)
dd_str['key1'] += 'a'
print(dd_str)

```
[[defaultdict 응용]]

# get함수 이용

```python
row = "1, 2, 3, 4, 5, 1, 2, 3, 4, 5\n"
print(row)

m_row = row.strip('\n').strip().split(", ")

dictionary = {}
print(m_row)
for word in m_row:
    if word:
        dictionary[word] = dictionary.get(word, 0) + 1


print(dictionary)
hello = {"a": 1, "b": 2}

# hello["c"] = hello.get("c")
hello["c"] = hello.get("c", 0)
hello["c"] += 1

print(hello)
```

여기서 data를 추가할 때 원래는 index를 이용해야 한다고 이해했지만, index뿐만이 아니라 get을 이용해서 위와 같이 추가할 수 있다.

dictionary에서 get을 이용할 때 아무것도 없으면 none을 반환하지만,

	.get("",0)을 이용한다면 0을 반환한다
그래서 추가적인 연산이 가능해진다.

# index로 직접 추가하기

```python
for index in range(len(row)):
            if row[index] not in dictionary and row:
                dictionary[row[index]] = 0
            dictionary[row[index]] += 1
```

이렇게 사용하는 것도 가능하다! 근데 공백을 확인해야 할 때는 get이 더 좋을 듯하다

# index로 직접 추가하기2

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
