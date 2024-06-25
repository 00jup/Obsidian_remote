
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










