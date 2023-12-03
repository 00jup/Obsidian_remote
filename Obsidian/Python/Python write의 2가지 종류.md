
# 1
```python
list = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

with open("test.csv", "w") as f:
    for row in list:
        f.write(f"{row[0],row[1],row[2]}\n")

with open("test.csv", "r") as f:
    # print(f.read()) 이것도 안 좋은 습관이 될 수 있다.
    output = f.readline()
    while output:
        print(output, end="")
        output = f.readline()

```

# 2
```python
list = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

with open("test.csv", "w") as f:
    for row in list:
        f.write(f"{row[0],row[1],row[2]}\n")

with open("test.csv", "r") as f:
    # print(f.read()) 이것도 안 좋은 습관이 될 수 있다.
    output = f.readline()
    while output:
        print(output, end="")
        output = f.readline()

```

        f.write(f"{row[0],row[1],row[2]}\n")
        f.write(f"{row[0],row[1],row[2]}\n")

둘은 데이터 저장하는 방식이 다르다
아래의 저장 방식은 괄호가 포함되어 저장된다.