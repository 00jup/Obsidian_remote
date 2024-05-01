

# CONCAT

SELECT CONCAT('h', 'j', 'i');

select를 적어야 결과를 얻을 수 있다.

# CONCAT_WS

```sql
mysql> SELECT CONCAT_WS('!', 'hi', 'bye', 'lol');
+------------------------------------+
| CONCAT_WS('!', 'hi', 'bye', 'lol') |
+------------------------------------+
| hi!bye!lol                         |
+------------------------------------+
1 row in set (0.00 sec)
```

사이로 들어간다.

# SUBSTRING (SUBSTR)
```sql
SELECT
    CONCAT (
        SUBSTR (author_fname, 1, 1),
        '.',
        SUBSTR (author_lname, 1, 1),
        '.'
    ) AS author_initials
FROM
    books;
```

# REPLACE
```sql
mysql> SELECT REPLACE('I am Park', 'Park', 10);
+----------------------------------+
| REPLACE('I am Park', 'Park', 10) |
+----------------------------------+
| I am 10                          |
+----------------------------------+
1 row in set (0.00 sec)

mysql> SELECT REPLACE(title, ' ', '-') FROM books;
+-----------------------------------------------------+
| REPLACE(title, ' ', '-')                            |
+-----------------------------------------------------+
| The-Namesake                                        |
| Norse-Mythology                                     |
| American-Gods                                       |
| Interpreter-of-Maladies                             |
| A-Hologram-for-the-King:-A-Novel                    |
| The-Circle                                          |
| The-Amazing-Adventures-of-Kavalier-&-Clay           |
| Just-Kids                                           |
| A-Heartbreaking-Work-of-Staggering-Genius           |
| Coraline                                            |
| What-We-Talk-About-When-We-Talk-About-Love:-Stories |
| Where-I'm-Calling-From:-Selected-Stories            |
| White-Noise                                         |
| Cannery-Row                                         |
| Oblivion:-Stories                                   |
| Consider-the-Lobster                                |
+-----------------------------------------------------+
16 rows in set (0.00 sec)
```


# REVERSE
```sql
mysql> SELECT REVERSE("chicken nuggest");
+----------------------------+
| REVERSE("chicken nuggest") |
+----------------------------+
| tseggun nekcihc            |
+----------------------------+
1 row in set (0.00 sec)

mysql> SELECT REVERSE(NULL);
+---------------+
| REVERSE(NULL) |
+---------------+
| NULL          |
+---------------+
1 row in set (0.00 sec)
```

# LENGTH
```sql
mysql> SELECT CHAR_LENGTH('Hello World');
+----------------------------+
| CHAR_LENGTH('Hello World') |
+----------------------------+
|                         11 |
+----------------------------+
1 row in set (0.00 sec)

mysql> SELECT LENGTH('Hey!');
+----------------+
| LENGTH('Hey!') |
+----------------+
|              4 |
+----------------+
1 row in set (0.00 sec)
```

LENGTH는 byte의 크기로 return해서 한자 같은 거 넣으면 다르게 나온다.
```sql
mysql> SELECT CONCAT(author_lname, ' is ', CHAR_LENGTH(author_lname)) AS len FROM books;
+----------------------+
| len                  |
+----------------------+
| Lahiri is 6          |
| Gaiman is 6          |
| Gaiman is 6          |
| Lahiri is 6          |
| Eggers is 6          |
| Eggers is 6          |
| Chabon is 6          |
| Smith is 5           |
| Eggers is 6          |
| Gaiman is 6          |
| Carver is 6          |
| Carver is 6          |
| DeLillo is 7         |
| Steinbeck is 9       |
| Foster Wallace is 14 |
| Foster Wallace is 14 |
+----------------------+
16 rows in set (0.00 sec)

mysql> SELECT author_lanme, CHAR_LENGTH(author_lname) AS 'Len' FROM books;
ERROR 1054 (42S22): Unknown column 'author_lanme' in 'field list'
mysql> SELECT author_lname, CHAR_LENGTH(author_lname) AS 'Len' FROM books;
+----------------+------+
| author_lname   | Len  |
+----------------+------+
| Lahiri         |    6 |
| Gaiman         |    6 |
| Gaiman         |    6 |
| Lahiri         |    6 |
| Eggers         |    6 |
| Eggers         |    6 |
| Chabon         |    6 |
| Smith          |    5 |
| Eggers         |    6 |
| Gaiman         |    6 |
| Carver         |    6 |
| Carver         |    6 |
| DeLillo        |    7 |
| Steinbeck      |    9 |
| Foster Wallace |   14 |
| Foster Wallace |   14 |
+----------------+------+
16 rows in set (0.01 sec)
```

# INSERT, TRIM