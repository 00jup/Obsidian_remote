
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

```sql
ALTER TABLE companies
DROP COLUMN city
```

delete가 아니라 DROP임

# Renaming Tables

```sql
show tables;

RENAME TABLE companies TO suppliers;
```


```sql
ALTER TABLE suppliers RENAME TO companies;
```

# Renaming Columns

```sql
ALTER TABLE suppliers
DESC companies;
RENAME COLUMN 
```

여기서 column은 optional이 아님