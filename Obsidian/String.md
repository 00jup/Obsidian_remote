

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