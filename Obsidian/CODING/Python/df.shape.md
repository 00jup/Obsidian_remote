
```python
df = pd.DataFrame({'Date':['10/2/2011', '11/2/2011', '12/2/2011'], 
                    'Phrases':['I have a cool family', 'I like avocados', 'I would like to go to school']})


df
Out[26]: 
        Date                       Phrases
0  10/2/2011          I have a cool family
1  11/2/2011               I like avocados
2  12/2/2011  I would like to go to school

df.shape
Out[27]: (3, 2)

df.shape[0]   #number of rows
Out[28]: 3

df.shape[1]   #number of columns
Out[29]: 2
```

`df.shape[0]` -> 열의 수

`df.shape[1]` -> 행의 수

