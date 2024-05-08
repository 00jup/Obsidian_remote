```python
order = {}

for i in range(6):
    # name, price = map(str, input("물건"), int, input("가격"))
    name, price = input("물건 이름과 금액 입력 : ").split()
    order[name] = int(price)

sum = 0

for i in order.values():
    sum += i


print(str(sum)+"원")

```

위 코드를 아래와 같이 바꿀 수 있다.

```python
order = {name: int(price) for _ in range(6) for name, price in [
    input("물건 이름과 가격을 띄어쓰기로 구분하여 입력하세요: ").split()]}
total_price = sum(order.values())
print(f"{total_price}원")
```

진짜 python은 미친 거 같다.....