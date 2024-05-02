
# subquery 라는 거임

subquery run first and run another query

```sql
mysql> SELECT title, pages FROM books WHERE pages = (SELECT MAX(pages) FROM books)
    -> ;
+-------------------------------------------+-------+
| title                                     | pages |
+-------------------------------------------+-------+
| The Amazing Adventures of Kavalier & Clay |   634 |
+-------------------------------------------+-------+
1 row in set (0.01 sec)

mysql> SELECT title, pages FROM books ORDER BY 2 DESC LIMIT 1;
+-------------------------------------------+-------+
| title                                     | pages |
+-------------------------------------------+-------+
| The Amazing Adventures of Kavalier & Clay |   634 |
+-------------------------------------------+-------+
```

위와 같이 2가지 방법이 존재함.

```sql
mysql> INSERT INTO books(title, pages) VALUES('my life in words', 634);
Query OK, 1 row affected (0.01 sec)

mysql> SELECT title, pages FROM books WHERE pages = (SELECT MAX(pages) FROM books);
+-------------------------------------------+-------+
| title                                     | pages |
+-------------------------------------------+-------+
| The Amazing Adventures of Kavalier & Clay |   634 |
| my life in words                          |   634 |
+-------------------------------------------+-------+
```

첫번째 방법을 사용하면 limit로 한개를 제한하지 않고 이렇게 데이터를 추가해도 자동으로 늘어나서 출력된다.