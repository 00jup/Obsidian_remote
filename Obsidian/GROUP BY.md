
[[groupby 잘 사용하기!]]

```sql
mysql> SELECT author_lname FROM books GROUP BY author_lname;
```

author_lname에 따라서 group by가 일어나는 거임.

```sql
mysql> SELECT author_lname FROM books GROUP BY 1;
```

이것도 가능함

DISTINCT랑 다르게 뒤에서 더 많은 것이 일어난다

```sql
mysql> SELECT author_lname, COUNT(*) FROM books GROUP BY 1;
+----------------+----------+
| author_lname   | COUNT(*) |
+----------------+----------+
| Lahiri         |        2 |
| Gaiman         |        3 |
| Eggers         |        3 |
| Chabon         |        1 |
| Smith          |        1 |
| Carver         |        2 |
| DeLillo        |        1 |
| Steinbeck      |        1 |
| Foster Wallace |        2 |
| Harris         |        2 |
| Saunders       |        1 |
| NULL           |        2 |
+----------------+----------+
12 rows in set (0.01 sec)
```

그래서 이런 결과가 나온다는 거 알 수 있음