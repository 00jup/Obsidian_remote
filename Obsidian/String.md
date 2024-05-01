

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

# INSERT, RIGTH, REFT, REPEAT, TRIM

```sql
SELECT INSERT('Hello Bobby', 6, 0, 'There'); 
 
SELECT LEFT('omghahalol!', 3);
 
SELECT RIGHT('omghahalol!', 4);
 
SELECT REPEAT('ha', 4);
 
SELECT TRIM('  pickle  ');
```

```sql
mysql> SELECT INSERT('Hello Bobby', 6, 0, 'There');
+--------------------------------------+
| INSERT('Hello Bobby', 6, 0, 'There') |
+--------------------------------------+
| HelloThere Bobby                     |
+--------------------------------------+
1 row in set (0.00 sec)

mysql> SELECT INSERT('Hello Bobby', 6, 4, 'There');
+--------------------------------------+
| INSERT('Hello Bobby', 6, 4, 'There') |
+--------------------------------------+
| HelloThereby                         |
+--------------------------------------+
1 row in set (0.00 sec)

mysql> SELECT INSERT('Hello Bobby', 6, 4, 'There');
+--------------------------------------+
| INSERT('Hello Bobby', 6, 4, 'There') |
+--------------------------------------+
| HelloThereby                         |
+--------------------------------------+
1 row in set (0.00 sec)

mysql> SELECT INSERT('Hello Bobby', 6, 6, 'There');
+--------------------------------------+
| INSERT('Hello Bobby', 6, 6, 'There') |
+--------------------------------------+
| HelloThere                           |
+--------------------------------------+
1 row in set (0.00 sec)

mysql>
mysql>
mysql> SELECT LEFT('omghahahlol!', 3);
+-------------------------+
| LEFT('omghahahlol!', 3) |
+-------------------------+
| omg                     |
+-------------------------+
1 row in set (0.00 sec)

mysql> SELECT RIGNT('omghahalol!', 4);
ERROR 1305 (42000): FUNCTION book_shop.RIGNT does not exist
mysql> SELECT RIGHT('omghahalol!', 4);
+-------------------------+
| RIGHT('omghahalol!', 4) |
+-------------------------+
| lol!                    |
+-------------------------+
1 row in set (0.00 sec)

mysql> SELECT LEFT(author_lname, 1) FROM books;
+-----------------------+
| LEFT(author_lname, 1) |
+-----------------------+
| L                     |
| G                     |
| G                     |
| L                     |
| E                     |
| E                     |
| C                     |
| S                     |
| E                     |
| G                     |
| C                     |
| C                     |
| D                     |
| S                     |
| F                     |
| F                     |
+-----------------------+
16 rows in set (0.00 sec)

mysql> SELECT REPEAT('ha', 4);
+-----------------+
| REPEAT('ha', 4) |
+-----------------+
| hahahaha        |
+-----------------+
1 row in set (0.00 sec)

mysql> SELECT TRIM('           boston     ');
+--------------------------------+
| TRIM('           boston     ') |
+--------------------------------+
| boston                         |
+--------------------------------+
1 row in set (0.00 sec)

mysql> SELECT TRIM('           boston    d   ');
+-----------------------------------+
| TRIM('           boston    d   ') |
+-----------------------------------+
| boston    d                       |
+-----------------------------------+
1 row in set (0.00 sec)

mysql> SELECT TRIM('....san antonio..');
+---------------------------+
| TRIM('....san antonio..') |
+---------------------------+
| ....san antonio..         |
+---------------------------+
1 row in set (0.00 sec)

mysql> SELECT TRIM(LEADING '.' FROM '....san antonio..');
+--------------------------------------------+
| TRIM(LEADING '.' FROM '....san antonio..') |
+--------------------------------------------+
| san antonio..                              |
+--------------------------------------------+
1 row in set (0.00 sec)

mysql> SELECT TRIM(TRAILING  FROM '....san antonio..');
+------------------------------------------+
| TRIM(TRAILING  FROM '....san antonio..') |
+------------------------------------------+
| ....san antonio..                        |
+------------------------------------------+
1 row in set (0.00 sec)

mysql> SELECT TRIM(TRAILING '.' FROM '....san antonio..');
+---------------------------------------------+
| TRIM(TRAILING '.' FROM '....san antonio..') |
+---------------------------------------------+
| ....san antonio                             |
+---------------------------------------------+
1 row in set (0.00 sec)

mysql> SELECT TRIM(BOTH'.' FROM '....san antonio..');
+----------------------------------------+
| TRIM(BOTH'.' FROM '....san antonio..') |
+----------------------------------------+
| san antonio                            |
+----------------------------------------+
1 row in set (0.01 sec)

```

# formatting을 하는 이유

```sql
SELECT 
    CONCAT(SUBSTR(title, 1, 10), '...') AS short_title,
    CONCAT(author_lname, ',', author_fname) AS author,
    CONCAT(stock_quantity, ' in stock') AS quantity
FROM
    books;
```

이게 아래보다 보기 편함

```sql
SELECT INSERT(title, 11,100, '...') AS 'short title', CONCAT(author_lname, ',', author_fname) AS
author, CONCAT(stock_quantity ,'in stock')AS 'quantity' FROM books;
```