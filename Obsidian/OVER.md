
## NTITLE
```mysql
SELECT 
	emp_no,
	department,
	salary,
	NTITLE(4) OVER(PARTITION BY department ORDER BY salary DESC) as dept_salary_quartile,
	NTITLE(4) OVER(PARTITION BY department ORDER BY salary DESC) as salary_quartile
FROM employees;
```

4개로 quartile을 나눠준다.

## FIRST_VALUE(emp_no)
```mysql
mysql> SELECT
    ->     emp_no,
    ->     department,
    ->     salary,
    ->     FIRST_VALUE(emp_no) OVER(PARTITION BY department ORDER BY salary DESC) as highest_paid_dept,
    ->     FIRST_VALUE(emp_no) OVER(ORDER BY salary DESC) as highest_paid_overall
    -> FROM employees;
+--------+------------------+--------+-------------------+----------------------+
| emp_no | department       | salary | highest_paid_dept | highest_paid_overall |
+--------+------------------+--------+-------------------+----------------------+
|     10 | sales            | 159000 |                10 |                   10 |
|      4 | engineering      | 103000 |                 4 |                   10 |
|      7 | engineering      |  91000 |                 4 |                   10 |
|      6 | engineering      |  89000 |                 4 |                   10 |
|      1 | engineering      |  80000 |                 4 |                   10 |
|     11 | sales            |  72000 |                10 |                   10 |
|      3 | engineering      |  70000 |                 4 |                   10 |
|      9 | sales            |  70000 |                10 |                   10 |
|      2 | engineering      |  69000 |                 4 |                   10 |
|      5 | engineering      |  67000 |                 4 |                   10 |
|     17 | customer service |  61000 |                17 |                   10 |
|     13 | sales            |  61000 |                10 |                   10 |
|     14 | sales            |  61000 |                10 |                   10 |
|     12 | sales            |  60000 |                10 |                   10 |
|      8 | sales            |  59000 |                10 |                   10 |
|     20 | customer service |  56000 |                17 |                   10 |
|     21 | customer service |  55000 |                17 |                   10 |
|     16 | customer service |  45000 |                17 |                   10 |
|     18 | customer service |  40000 |                17 |                   10 |
|     15 | customer service |  38000 |                17 |                   10 |
|     19 | customer service |  31000 |                17 |                   10 |
+--------+------------------+--------+-------------------+----------------------+
```

```mysql
SELECT 
    emp_no, 
    department, 
    salary,
    FIRST_VALUE(emp_no) OVER(PARTITION BY department ORDER BY salary DESC) as highest_paid_dept,
    FIRST_VALUE(emp_no) OVER(ORDER BY salary DESC) as highest_paid_overall
FROM employees;
```


```mysql
SELECT 
    emp_no, 
    department, 
    salary,
    FIRST_VALUE(emp_no) OVER(PARTITION BY department ORDER BY salary DESC) as highest_paid_dept
FROM employees ORDER BY salary DESC;
```





