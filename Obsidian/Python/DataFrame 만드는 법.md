
> data = pd.read_csv("titanic.csv")

## Version 0 groupby로 정리하기
```python
data = data[["Age-Range", "Survived", "Fare"]].dropna()
data = data.groupby(["Survived", "Age-Range"]).mean()
```

## Version 1 index, columns 직접 설정하기

```python
new_data = pd.DataFrame(index=[0, 10, 20, 30, 40, 50, 60, 70, 80],
                        columns=["Dead", "Survived"])

new_data['Dead'] = data.loc[0]
new_data['Survived'] = data.loc[1]

new_data = new_data.fillna(value=0)
```


## Version 2 pivot table

```python
new_data2 = data.pivot_table(index='Age-Range',
                             columns=["Survived"],
                             values="Fare",
                             aggfunc='mean')  # .melt()
```

