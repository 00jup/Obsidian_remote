

```mysql
SELECT (SELECT Count(*) 
        FROM   photos) / (SELECT Count(*) 
                          FROM   users) AS avg; 
```

위와 같이 바로 계산해서 사용하는 것이 가능함.