
# Code
```python

name = input("이름을 입력하세요 : ")
st_id = input("학번을 입력하세요 : ")
count = 0

def print_name_id(name,id):
    print("이름 : {} 학번 : {}".format(name, st_id))


print_name_id(name, st_id)

def count_zero(st_id):
    for num in st_id:
        if num == '0':
            count += 1
    
    return count
    
    

print(count_zero(st_id))
```

위에서 count와 같이 전역변수로 사용하려면 아래와 같이 수정해야 한다.

```python

name = input("이름을 입력하세요 : ")
st_id = input("학번을 입력하세요 : ")
count = 0

def print_name_id(name,id):
    print("이름 : {} 학번 : {}".format(name, st_id))


print_name_id(name, st_id)

def count_zero(st_id):
	global count
    for num in st_id:
        if num == '0':
            count += 1
    
    return count
    
    

print(count_zero(st_id))
```

