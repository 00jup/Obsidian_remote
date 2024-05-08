
```sql
mysql>
mysql> INSERT INTO products(price) VALUES (1.112312);
Query OK, 1 row affected, 1 warning (0.01 sec)

mysql> SHOW WARNINGS;
+-------+------+--------------------------------------------+
| Level | Code | Message                                    |
+-------+------+--------------------------------------------+
| Note  | 1265 | Data truncated for column 'price' at row 1 |
+-------+------+--------------------------------------------+
1 row in set (0.00 sec)
```