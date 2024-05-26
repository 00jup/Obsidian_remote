
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
RENAME COLUMN name TO company_name;
```

여기서 column은 optional이 아님

```sql
mysql> DESC suppilers
    -> ;
ERROR 1146 (42S02): Table 'pet_shop.suppilers' doesn't exist
mysql> DESC suppliers
    -> ;
+---------+--------------+------+-----+---------+-------+
| Field   | Type         | Null | Key | Default | Extra |
+---------+--------------+------+-----+---------+-------+
| name    | varchar(255) | NO   | PRI | NULL    |       |
| address | varchar(255) | NO   | PRI | NULL    |       |
| city    | varchar(25)  | YES  |     | NULL    |       |
+---------+--------------+------+-----+---------+-------+
3 rows in set (0.01 sec)

mysql> ALTER TABLE suppliers
    -> RENAME COLUMN name TO company_name;
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> DESC suppliers
    -> ;
+--------------+--------------+------+-----+---------+-------+
| Field        | Type         | Null | Key | Default | Extra |
+--------------+--------------+------+-----+---------+-------+
| company_name | varchar(255) | NO   | PRI | NULL    |       |
| address      | varchar(255) | NO   | PRI | NULL    |       |
| city         | varchar(25)  | YES  |     | NULL    |       |
+--------------+--------------+------+-----+---------+-------+
3 rows in set (0.01 sec)

```

# Modify Column

```sql
ALTER TABLE suppliers
MODIFY biz_name VARCHAR(100);
```


