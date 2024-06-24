
JOIN 으로 만든 테이블을 view에서 업데이트 하거나 지울 수 없다.

VIEW에서 

```mysql
CREATE OR REPLACE VIEW ordered_series AS
SELECT * FROM series ORDER BY released_year DESC
```

## ALTER TABLE

```mysql
ALTER VIEW ordered_series AS
SELECT * FROM series ORDER BY released_year DESC
```

## HAVING
```mysql
SELECT
	title,
	AVG(rating)
FROM full_reviews
GROUP BY title HAVING COUNT(rating) > 1;
```

GROUP BY를 사용 후에 HAVING으로 정리가 가능하다.

## ROLLUP
```mysql
mysql> SELECT title, AVG(rating) FROM full_reviews GROUP BY title WITH ROLLUP;
+----------------------+-------------+
| title                | AVG(rating) |
+----------------------+-------------+
| Archer               |     8.12000 |
| Arrested Development |     8.08000 |
| Bob's Burgers        |     7.52000 |
| Bojack Horseman      |     7.94000 |
| Breaking Bad         |     9.36000 |
| Curb Your Enthusiasm |     8.12000 |
| Fargo                |     9.40000 |
| Freaks and Geeks     |     8.60000 |
| General Hospital     |     5.38000 |
| Halt and Catch Fire  |     9.90000 |
| Seinfeld             |     7.60000 |
| Stranger Things      |     8.76667 |
| NULL                 |     8.02553 |
+----------------------+-------------+
13 rows in set (0.00 sec)
```


```mysql
SELECT released_year, AVG(rating) FROM full_reviews GROUP BY released_year, genre WITH ROLLUP;
```


## SET MODE
```mysql
-- To View Modes:
SELECT @@GLOBAL.sql_mode;
SELECT @@SESSION.sql_mode;
 
-- To Set Them:
SET GLOBAL sql_mode = 'modes';
SET SESSION sql_mode = 'modes';
```

## OVER
```mysql
SELECT 
    emp_no, 
    department, 
    salary, 
    MIN(salary) OVER(),
    MAX(salary) OVER()
FROM employees;
```

원래 GROUP BY 해야 하는데 OVER를 사용하면 바로 사용이 가능하다