
```sql
mysql> SELECT book_id, title, released_year FROM books ORDER BY 2 LIMIT 5;
+---------+-------------------------------------------+---------------+
| book_id | title                                     | released_year |
+---------+-------------------------------------------+---------------+
|      17 | 10% Happier                               |          2014 |
|       9 | A Heartbreaking Work of Staggering Genius |          2001 |
|       5 | A Hologram for the King: A Novel          |          2012 |
|       3 | American Gods                             |          2001 |
|      14 | Cannery Row                               |          1945 |
+---------+-------------------------------------------+---------------+
5 rows in set (0.00 sec)
```

```sql
mysql> SELECT book_id, title, released_year FROM books ORDER BY released_year DESC LIMIT 2,5;
```

2부터 5개만 보여줘라!