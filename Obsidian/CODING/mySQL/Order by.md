
```sql
SELECT author_lname FROM books ORDER BY author_lname;
```

column을 숫자로 나타낼 수도 있음

```sql
mysql> SELECT book_id, author_fname, author_lname, pages FROM books ORDER BY pages;
+---------+--------------+----------------+-------+
| book_id | author_fname | author_lname   | pages |
+---------+--------------+----------------+-------+
|      20 | NULL         | steele         |  NULL |
|      11 | Raymond      | Carver         |   176 |
|      14 | John         | Steinbeck      |   181 |
|       4 | Jhumpa       | Lahiri         |   198 |
|      10 | Neil         | Gaiman         |   208 |
|      17 | Dan          | Harris         |   256 |
|       1 | Jhumpa       | Lahiri         |   291 |
|       2 | Neil         | Gaiman         |   304 |
|       8 | Patti        | Smith          |   304 |
|      13 | Don          | DeLillo        |   320 |
|      15 | David        | Foster Wallace |   329 |
|      16 | David        | Foster Wallace |   343 |
|       5 | Dave         | Eggers         |   352 |
|      19 | George       | Saunders       |   367 |
|      18 | Freida       | Harris         |   428 |
|       9 | Dave         | Eggers         |   437 |
|       3 | Neil         | Gaiman         |   465 |
|       6 | Dave         | Eggers         |   504 |
|      12 | Raymond      | Carver         |   526 |
|       7 | Michael      | Chabon         |   634 |
+---------+--------------+----------------+-------+
20 rows in set (0.00 sec)

mysql> SELECT book_id, author_fname, author_lname, pages FROM books ORDER BY 4;
+---------+--------------+----------------+-------+
| book_id | author_fname | author_lname   | pages |
+---------+--------------+----------------+-------+
|      20 | NULL         | steele         |  NULL |
|      11 | Raymond      | Carver         |   176 |
|      14 | John         | Steinbeck      |   181 |
|       4 | Jhumpa       | Lahiri         |   198 |
|      10 | Neil         | Gaiman         |   208 |
|      17 | Dan          | Harris         |   256 |
|       1 | Jhumpa       | Lahiri         |   291 |
|       2 | Neil         | Gaiman         |   304 |
|       8 | Patti        | Smith          |   304 |
|      13 | Don          | DeLillo        |   320 |
|      15 | David        | Foster Wallace |   329 |
|      16 | David        | Foster Wallace |   343 |
|       5 | Dave         | Eggers         |   352 |
|      19 | George       | Saunders       |   367 |
|      18 | Freida       | Harris         |   428 |
|       9 | Dave         | Eggers         |   437 |
|       3 | Neil         | Gaiman         |   465 |
|       6 | Dave         | Eggers         |   504 |
|      12 | Raymond      | Carver         |   526 |
|       7 | Michael      | Chabon         |   634 |
+---------+--------------+----------------+-------+
20 rows in set (0.00 sec)

mysql> SELECT book_id, author_fname, author_lname, pages FROM books ORDER BY 4 DESC;
+---------+--------------+----------------+-------+
| book_id | author_fname | author_lname   | pages |
+---------+--------------+----------------+-------+
|       7 | Michael      | Chabon         |   634 |
|      12 | Raymond      | Carver         |   526 |
|       6 | Dave         | Eggers         |   504 |
|       3 | Neil         | Gaiman         |   465 |
|       9 | Dave         | Eggers         |   437 |
|      18 | Freida       | Harris         |   428 |
|      19 | George       | Saunders       |   367 |
|       5 | Dave         | Eggers         |   352 |
|      16 | David        | Foster Wallace |   343 |
|      15 | David        | Foster Wallace |   329 |
|      13 | Don          | DeLillo        |   320 |
|       2 | Neil         | Gaiman         |   304 |
|       8 | Patti        | Smith          |   304 |
|       1 | Jhumpa       | Lahiri         |   291 |
|      17 | Dan          | Harris         |   256 |
|      10 | Neil         | Gaiman         |   208 |
|       4 | Jhumpa       | Lahiri         |   198 |
|      14 | John         | Steinbeck      |   181 |
|      11 | Raymond      | Carver         |   176 |
|      20 | NULL         | steele         |  NULL |
+---------+--------------+----------------+-------+
```

```sql
mysql> SELECT author_lname, released_year, title FROM books ORDER BY 1,2;
```

굿굿 이렇게 사용하는 것도 가능함


```sql
mysql> SELECT CONCAT(author_fname, ' ',  author_lname) AS author FROM books ORDER BY 1;
```

이렇게 사용하는 것도 가능함!