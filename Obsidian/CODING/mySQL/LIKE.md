
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

_ -> 1 time

## __ %% 차이점
```sql
mysql> SELECT * FROM books WHERE author_fname LIKE '_a_';
+---------+-------------+--------------+--------------+---------------+----------------+-------+
| book_id | title       | author_fname | author_lname | released_year | stock_quantity | pages |
+---------+-------------+--------------+--------------+---------------+----------------+-------+
|      17 | 10% Happier | Dan          | Harris       |          2014 |             29 |   256 |
+---------+-------------+--------------+--------------+---------------+----------------+-------+
1 row in set (0.00 sec)

mysql> SELECT * FROM books WHERE author_fname LIKE '%a%';
+---------+-----------------------------------------------------+--------------+----------------+---------------+----------------+-------+
| book_id | title                                               | author_fname | author_lname   | released_year | stock_quantity | pages |
+---------+-----------------------------------------------------+--------------+----------------+---------------+----------------+-------+
|       1 | The Namesake                                        | Jhumpa       | Lahiri         |          2003 |             32 |   291 |
|       4 | Interpreter of Maladies                             | Jhumpa       | Lahiri         |          1996 |             97 |   198 |
|       5 | A Hologram for the King: A Novel                    | Dave         | Eggers         |          2012 |            154 |   352 |
|       6 | The Circle                                          | Dave         | Eggers         |          2013 |             26 |   504 |
|       7 | The Amazing Adventures of Kavalier & Clay           | Michael      | Chabon         |          2000 |             68 |   634 |
|       8 | Just Kids                                           | Patti        | Smith          |          2010 |             55 |   304 |
|       9 | A Heartbreaking Work of Staggering Genius           | Dave         | Eggers         |          2001 |            104 |   437 |
|      11 | What We Talk About When We Talk About Love: Stories | Raymond      | Carver         |          1981 |             23 |   176 |
|      12 | Where I'm Calling From: Selected Stories            | Raymond      | Carver         |          1989 |             12 |   526 |
|      15 | Oblivion: Stories                                   | David        | Foster Wallace |          2004 |            172 |   329 |
|      16 | Consider the Lobster                                | David        | Foster Wallace |          2005 |             92 |   343 |
|      17 | 10% Happier                                         | Dan          | Harris         |          2014 |             29 |   256 |
|      18 | fake_book                                           | Freida       | Harris         |          2001 |            287 |   428 |
+---------+-----------------------------------------------------+--------------+----------------+---------------+----------------+-------+
13 rows in set (0.00 sec)
```

## escape
```sql
-- To select books with '%' in their title:
SELECT * FROM books
WHERE title LIKE '%\%%';
 
-- To select books with an underscore '_' in title:
SELECT * FROM books
WHERE title LIKE '%\_%';
```