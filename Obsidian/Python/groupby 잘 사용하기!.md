

```python
data = data.astype({"Age-band": int})
data = data[["Age-band", "Fare", "Survived"]]

data = data.groupby(["Survived", "Age-band"]).mean()
# 순서 맞춰서 적는 습관가지기
```

groupby의 경우 원하는 대로 커스텀이 가능하다.

하지만 순서대로 적는 게 이해하기 편하기 때문에 그렇게 적도록 하자

더불어 사용하기 전에 필요없는 데이터는 제거하고 사용하는 게 좋은 건가?