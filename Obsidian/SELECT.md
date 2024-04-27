
SELECT * FROM cats;

SELECT name, age FROM cats;

SELECT name, breed FROM cats;

`SELECT name FROM WHERE age=4;`

age = 4를 쓰니까 앞에서 age column이 없어도 사용 가능하다.

### 예시
```sql
mysql> SELECT name, age FROM cats WHERE breed = 'Tabby';
+-------+------+
| name  | age  |
+-------+------+
| Ringo |    4 |
| Misty |   13 |
+-------+------+
2 rows in set (0.00 sec)

mysql> SELECT cat_id, age FROM cats WHERE cat_id = age;
+--------+------+
| cat_id | age  |
+--------+------+
|      4 |    4 |
|      7 |    7 |
+--------+------+
2 rows in set (0.00 sec)
```
