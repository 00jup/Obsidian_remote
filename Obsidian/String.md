

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

