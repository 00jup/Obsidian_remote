
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

```sql
mysql> SELECT author_lname, COUNT(*) AS books_written FROM books GROUP BY 1 ORDER BY 2 DESC;
+----------------+---------------+
| author_lname   | books_written |
+----------------+---------------+
| Gaiman         |             3 |
| Eggers         |             3 |
| Lahiri         |             2 |
| Carver         |             2 |
| Foster Wallace |             2 |
| Harris         |             2 |
| NULL           |             2 |
| Chabon         |             1 |
| Smith          |             1 |
| DeLillo        |             1 |
| Steinbeck      |             1 |
| Saunders       |             1 |
+----------------+---------------+
12 rows in set (0.00 sec)
```

이렇게 데이터를 가공하는 거다


## 주의
```sql
mysql> SELECT * FROM books GROUP BY author_lname;
```

이건 안 됨. all column을 선택하는 거니까
group은 하나의 column으로 하는 거임.