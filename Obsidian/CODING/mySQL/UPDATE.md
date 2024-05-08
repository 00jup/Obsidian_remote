
# Basic Pattern
UPDATE cats SET col=val, another_col_val WHERE name=~~ ;

```sql
mysql> DELETE FROM cats WHERE cat_id = 7;
Query OK, 1 row affected (0.01 sec)

mysql> SELECT * FROM cats
    -> ;
+--------+----------------+------------+------+
| cat_id | name           | breed      | age  |
+--------+----------------+------------+------+
|      1 | Ringo          | Tabby      |    4 |
|      2 | Cindy          | Maine Coon |   10 |
|      3 | Dumbledore     | Maine Coon |   11 |
|      4 | Egg            | Persian    |    4 |
|      5 | Misty          | Tabby      |   14 |
|      6 | George Michael | Ragdoll    |    9 |
+--------+----------------+------------+------+
6 rows in set (0.00 sec)

mysql> INSERT INTO cats(name, breed, age) VALUES ('Jackson', 'Sphynx', 7);
Query OK, 1 row affected (0.00 sec)

mysql> SELECT * FROM cats
    -> ;
+--------+----------------+------------+------+
| cat_id | name           | breed      | age  |
+--------+----------------+------------+------+
|      1 | Ringo          | Tabby      |    4 |
|      2 | Cindy          | Maine Coon |   10 |
|      3 | Dumbledore     | Maine Coon |   11 |
|      4 | Egg            | Persian    |    4 |
|      5 | Misty          | Tabby      |   14 |
|      6 | George Michael | Ragdoll    |    9 |
|      8 | Jackson        | Sphynx     |    7 |
+--------+----------------+------------+------+
7 rows in set (0.01 sec)

mysql> UPDATE cats SET name="Jack" WHERE name = 'Jackson';
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> SELECT * FROM cats
    -> ;
+--------+----------------+------------+------+
| cat_id | name           | breed      | age  |
+--------+----------------+------------+------+
|      1 | Ringo          | Tabby      |    4 |
|      2 | Cindy          | Maine Coon |   10 |
|      3 | Dumbledore     | Maine Coon |   11 |
|      4 | Egg            | Persian    |    4 |
|      5 | Misty          | Tabby      |   14 |
|      6 | George Michael | Ragdoll    |    9 |
|      8 | Jack           | Sphynx     |    7 |
+--------+----------------+------------+------+
7 rows in set (0.01 sec)

mysql> UPDATE cats SET breed = "British Shorthair" WHERE breed = "Tabby";
Query OK, 2 rows affected (0.00 sec)
Rows matched: 2  Changed: 2  Warnings: 0

mysql> SELECT * FROM cats;
+--------+----------------+-------------------+------+
| cat_id | name           | breed             | age  |
+--------+----------------+-------------------+------+
|      1 | Ringo          | British Shorthair |    4 |
|      2 | Cindy          | Maine Coon        |   10 |
|      3 | Dumbledore     | Maine Coon        |   11 |
|      4 | Egg            | Persian           |    4 |
|      5 | Misty          | British Shorthair |   14 |
|      6 | George Michael | Ragdoll           |    9 |
|      8 | Jack           | Sphynx            |    7 |
+--------+----------------+-------------------+------+
7 rows in set (0.01 sec)

mysql> UPDATE cats SET age = 12 WHERE breed = "Maine Coon";
Query OK, 2 rows affected (0.00 sec)
Rows matched: 2  Changed: 2  Warnings: 0

mysql> SELECT * FROM cats;
+--------+----------------+-------------------+------+
| cat_id | name           | breed             | age  |
+--------+----------------+-------------------+------+
|      1 | Ringo          | British Shorthair |    4 |
|      2 | Cindy          | Maine Coon        |   12 |
|      3 | Dumbledore     | Maine Coon        |   12 |
|      4 | Egg            | Persian           |    4 |
|      5 | Misty          | British Shorthair |   14 |
|      6 | George Michael | Ragdoll           |    9 |
|      8 | Jack           | Sphynx            |    7 |
+--------+----------------+-------------------+------+
7 rows in set (0.00 sec)
```