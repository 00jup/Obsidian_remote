

```sql
mysql> SELECT DISTINCT author_fname, author_lname, released_year FROM books;
+--------------+----------------+---------------+
| author_fname | author_lname   | released_year |
+--------------+----------------+---------------+
| Jhumpa       | Lahiri         |          2003 |
| Neil         | Gaiman         |          2016 |
| Neil         | Gaiman         |          2001 |
| Jhumpa       | Lahiri         |          1996 |
| Dave         | Eggers         |          2012 |
| Dave         | Eggers         |          2013 |
| Michael      | Chabon         |          2000 |
| Patti        | Smith          |          2010 |
| Dave         | Eggers         |          2001 |
| Neil         | Gaiman         |          2003 |
| Raymond      | Carver         |          1981 |
| Raymond      | Carver         |          1989 |
| Don          | DeLillo        |          1985 |
| John         | Steinbeck      |          1945 |
| David        | Foster Wallace |          2004 |
| David        | Foster Wallace |          2005 |
| Dan          | Harris         |          2014 |
| Freida       | Harris         |          2001 |
| George       | Saunders       |          2017 |
+--------------+----------------+---------------+
```

released_year을 넣으면 row가 distinct해지니까 똑같은 이름도 나오는 거임