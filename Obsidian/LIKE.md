
`WHERE author_fname LIKE '%Dav%'`
SEARCHING에 도움을 준다.

David라는 이름을 정확하게 알아야 찾는 게 아니라 dav가 들어가 있는 문자열을 찾을 때 사용하는 거다. 정확히 모를 때 사용

```sql
mysql> SELECT title, author_fname, author_lname FROM books WHERE author_fname LIKE '%Dav%';
+-------------------------------------------+--------------+----------------+
| title                                     | author_fname | author_lname   |
+-------------------------------------------+--------------+----------------+
| A Hologram for the King: A Novel          | Dave         | Eggers         |
| The Circle                                | Dave         | Eggers         |
| A Heartbreaking Work of Staggering Genius | Dave         | Eggers         |
| Oblivion: Stories                         | David        | Foster Wallace |
| Consider the Lobster                      | David        | Foster Wallace |
+-------------------------------------------+--------------+----------------+
5 rows in set (0.01 sec)
```

% -> optional 0 or more times

`4글자 인 거 찾을 때`
```sql
mysql> SELECT * FROM books WHERE author_fname LIKE '____';
```

## 