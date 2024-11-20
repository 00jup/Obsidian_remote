```python
def generate_even_numbers(limit):
   num = 0
   while num < limit:
       yield num
       num += 2

for number in generate_even_numbers(10):
   print(number)
```

여기서 yield를 없앤다면?

```python
def generate_even_numbers(limit):
   num = 0
   while num < limit:
       num += 2

for number in generate_even_numbers(10):
   print(number)
```

작동 안 함

return을 넣어도 num 값이 저장되는 게 아니라서 0, 2, 4, 6, 8 이렇게 출력되지 않는다.