
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


```sql
mysql> ALTER TABLE suppliers MODIFY company_name VARCHAR(100) DEFAULT 'unknown';
Query OK, 1 row affected (0.03 sec)
Records: 1  Duplicates: 0  Warnings: 0

mysql> DESC suppliers;
+--------------+--------------+------+-----+---------+-------+
| Field        | Type         | Null | Key | Default | Extra |
+--------------+--------------+------+-----+---------+-------+
| company_name | varchar(100) | YES  | MUL | unknown |       |
| address      | varchar(255) | NO   |     | NULL    |       |
| city         | varchar(25)  | YES  |     | NULL    |       |
+--------------+--------------+------+-----+---------+-------+
3 rows in set (0.01 sec)
```

근데 이거 하면 key가 MUL로 바뀜


```sql
ALTER TABLE suppliers
MODIFY biz_name name VARCHAR(100);
```

이렇게 하면 이름도 바꿀 수 있음

# ALTER TABLE에서 constraint 사용하기

```sql
ALTER TABLE houses ADD CONSTRAINT positive_pprice CHECK (purchase_price >= 0)
```

```sql
mysql> ALTER TABLE houses ADD CONSTRAINT positive_pprice CHECK (purchase_price >= 0);
Query OK, 1 row affected (0.03 sec)
Records: 1  Duplicates: 0  Warnings: 0

mysql> DESC houses;
+----------------+------+------+-----+---------+-------+
| Field          | Type | Null | Key | Default | Extra |
+----------------+------+------+-----+---------+-------+
| purchase_price | int  | NO   |     | NULL    |       |
| sale_price     | int  | NO   |     | NULL    |       |
+----------------+------+------+-----+---------+-------+
2 rows in set (0.00 sec)

mysql> INSERT INTO houses(purchase_price, sale_price) VALUES (-1, 4);
ERROR 3819 (HY000): Check constraint 'positive_pprice' is violated.
```

```sql
mysql> ALTER TABLE houses DROP CONSTRAINT positive_pprice;
Query OK, 0 rows affected (0.00 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> INSERT INTO houses(purchase_price, sale_price) VALUES (-1, 4);
Query OK, 1 row affected (0.00 sec)
```

이렇게 된다. DROP 하면

잘 쓰면 powerful 함.
![[Screenshot 2024-05-26 at 23.49.14.png]]

공식 문서에서 