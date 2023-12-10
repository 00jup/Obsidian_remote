```python
for i in range(5):
    if i > 10:
        print("i>10")
    # 출력될 일 없음
    # 한번도 이런 구문이 실행되지 않는다면 이걸 하세요 이렇게 만들 수 있다.
else:
    print("flag is True")
# 만약 이 안에서 흐름을 해치는 구문이 실행되면 이걸 실행해라
# 비밀번호 최대 3번 입력 다 틀리면? 아무것도 못하게 만들어야 하는데 그게 else안에 들어가는 것
```

try except를 배우다가 알게 된 사실인데

```python
try:
	D = int(input(""))
except D<0:
	print("Error occured!")
```
이거랑

```python
D = int(input(""))
if D<0:
	print("Error occured!")
```
이거랑 무슨 상관이 있을까 하다가
D<0일 때, exception을 주는 것은 방식의 차이인 것.
if를 섞어서 주는 거랑은 다름.
설명하는 방식이 다름
