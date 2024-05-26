
```sql
ALTER TABLE companies
ADD COLUMN city VARCHAR(25);
```

내가 원하는 column을 업데이트 할 수 있음.

default도 설정할 수 있다.

```sql
ALTER TABLE companies
ADD COLUMN employee_count INT NOT NULL DEFAULT 1;
```


# DROP

