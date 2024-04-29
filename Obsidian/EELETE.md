

```sql
mysql> DELETE FROM cats WHERE age = 4;
Query OK, 1 row affected (0.01 sec)

mysql> SELECT * FROM cats;
+--------+----------------+-------------------+------+
| cat_id | name           | breed             | age  |
+--------+----------------+-------------------+------+
|      2 | Cindy          | Maine Coon        |   12 |
|      3 | Dumbledore     | Maine Coon        |   12 |
|      5 | Misty          | British Shorthair |   14 |
|      6 | George Michael | Ragdoll           |    9 |
|      8 | Jack           | Sphynx            |    7 |
+--------+----------------+-------------------+------+
5 rows in set (0.00 sec)

mysql> DELETE FROM cats WHERE age=cat_id;
Query OK, 0 rows affected (0.00 sec)

mysql> DELETE FROM cats;
Query OK, 5 rows affected (0.00 sec)

mysql> SELECT * FROM cats;
Empty set (0.01 sec)
```