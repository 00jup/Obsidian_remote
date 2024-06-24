
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

원래 GROUP BY 해야 하는데 OVER를 사용하면 바로 사용이 가능하다.

```mysql
SELECT emp_no, department, salary, SUM(salary) OVER(PARTITION BY department), SUM(salary) OVER()
FROM employees;
```

```mysql
SELECT emp_no, department, salary, SUM(salary) OVER(PARTITION BY department ORDER BY salary) AS rolling_dept_salary, SUM(salary) OVER()
FROM employees;
```
더하는 과정을 볼 수 있음.

```mysql
mysql> SELECT emp_no, department, salary, MIN(salary) OVER(PARTITION BY department ORDER BY salary DESC) AS rolling_dept_salary, SUM(salary) OVER() FROM employees;
+--------+------------------+--------+---------------------+--------------------+
| emp_no | department       | salary | rolling_dept_salary | SUM(salary) OVER() |
+--------+------------------+--------+---------------------+--------------------+
|     17 | customer service |  61000 |               61000 |            1437000 |
|     20 | customer service |  56000 |               56000 |            1437000 |
|     21 | customer service |  55000 |               55000 |            1437000 |
|     16 | customer service |  45000 |               45000 |            1437000 |
|     18 | customer service |  40000 |               40000 |            1437000 |
|     15 | customer service |  38000 |               38000 |            1437000 |
|     19 | customer service |  31000 |               31000 |            1437000 |
|      4 | engineering      | 103000 |              103000 |            1437000 |
|      7 | engineering      |  91000 |               91000 |            1437000 |
|      6 | engineering      |  89000 |               89000 |            1437000 |
|      1 | engineering      |  80000 |               80000 |            1437000 |
|      3 | engineering      |  70000 |               70000 |            1437000 |
|      2 | engineering      |  69000 |               69000 |            1437000 |
|      5 | engineering      |  67000 |               67000 |            1437000 |
|     10 | sales            | 159000 |              159000 |            1437000 |
|     11 | sales            |  72000 |               72000 |            1437000 |
|      9 | sales            |  70000 |               70000 |            1437000 |
|     13 | sales            |  61000 |               61000 |            1437000 |
|     14 | sales            |  61000 |               61000 |            1437000 |
|     12 | sales            |  60000 |               60000 |            1437000 |
|      8 | sales            |  59000 |               59000 |            1437000 |
+--------+------------------+--------+---------------------+--------------------+
21 rows in set (0.00 sec)
```

```mysql
mysql> SELECT emp_no, department, salary, RANK() OVER(PARTITION BY department ORDER BY salary DESC) as dept_salary_rank, RANK() OVER(ORDER BY salary DESC) AS overall_salary_rank  FROM employees;
+--------+------------------+--------+------------------+---------------------+
| emp_no | department       | salary | dept_salary_rank | overall_salary_rank |
+--------+------------------+--------+------------------+---------------------+
|     10 | sales            | 159000 |                1 |                   1 |
|      4 | engineering      | 103000 |                1 |                   2 |
|      7 | engineering      |  91000 |                2 |                   3 |
|      6 | engineering      |  89000 |                3 |                   4 |
|      1 | engineering      |  80000 |                4 |                   5 |
|     11 | sales            |  72000 |                2 |                   6 |
|      3 | engineering      |  70000 |                5 |                   7 |
|      9 | sales            |  70000 |                3 |                   7 |
|      2 | engineering      |  69000 |                6 |                   9 |
|      5 | engineering      |  67000 |                7 |                  10 |
|     17 | customer service |  61000 |                1 |                  11 |
|     13 | sales            |  61000 |                4 |                  11 |
|     14 | sales            |  61000 |                4 |                  11 |
|     12 | sales            |  60000 |                6 |                  14 |
|      8 | sales            |  59000 |                7 |                  15 |
|     20 | customer service |  56000 |                2 |                  16 |
|     21 | customer service |  55000 |                3 |                  17 |
|     16 | customer service |  45000 |                4 |                  18 |
|     18 | customer service |  40000 |                5 |                  19 |
|     15 | customer service |  38000 |                6 |                  20 |
|     19 | customer service |  31000 |                7 |                  21 |
+--------+------------------+--------+------------------+---------------------+
21 rows in set (0.00 sec)
```

```mysql
SELECT 
	emp_no,
	department,
	salary,
	ROW_NUMBER() OVER(PARTITION BY department ORDER BY salary DESC) as row_number,
	RANK() OVER(PARTITION BY department ORDER BY salary DESC) as dept_salary_rank,
	DENSE_RANK() OVER(ORDER BY salary DESC) AS overall_dense_rank
FROM employees;

```