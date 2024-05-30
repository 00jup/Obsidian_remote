
1. one to one
![[Screenshot 2024-05-27 at 00.24.09 1.png]]


2.  one to many
![[Screenshot 2024-05-27 at 00.24.14.png]]


3.  many to many!
![[Screenshot 2024-05-27 at 00.24.17 1.png]]

# One to many Example
![[Screenshot 2024-05-27 at 00.27.12.png]]

order는 customer를 하나만 가지고 customer는 여러개 order를 가질 수 있다.

```sql
CREATE TABLE customers(
	id INT PRIMARY KEY AUTO_INCREMENT,
	first_name VARCHAR(50),
	last_name VARCHAR(50),
	email VARCHAR(50)
);

CREATE TABLE orders(
	id INT PRIMARY KEY AUTO_INCREMENT,
	order_date DATE,
	amount DECIMAL(8,2),
	customer_id INT
);
```

이렇게 해도 작동에는 이상없음.

```sql
CREATE TABLE customers(
	id INT PRIMARY KEY AUTO_INCREMENT,
	first_name VARCHAR(50),
	last_name VARCHAR(50),
	email VARCHAR(50)
);

CREATE TABLE orders(
	id INT PRIMARY KEY AUTO_INCREMENT,
	order_date DATE,
	amount DECIMAL(8,2),
	customer_id INT,
	FOREIGN KEY (customer_id) REFERENCES customers(id)
);
```

분리된 table이 어떻게 함께 작동하게 할까?

join을 사용

```sql
mysql> SELECT * FROM orders WHERE customer_id = (SELECT id FROM customers WHERE last_name = 'George');
+----+------------+--------+-------------+
| id | order_date | amount | customer_id |
+----+------------+--------+-------------+
|  1 | 2016-02-10 |  99.99 |           1 |
|  2 | 2017-11-11 |  35.50 |           1 |
+----+------------+--------+-------------+
2 rows in set (0.00 sec)
```
이렇게 사용하다.


## Cross JOIN
아래와 같이 하면 다 합쳐서 나오는데 이걸 해결하는 걸 배울 거임
```sql
mysql> SELECT * FROM customers, orders;
+----+------------+-----------+------------------+----+------------+--------+-------------+
| id | first_name | last_name | email            | id | order_date | amount | customer_id |
+----+------------+-----------+------------------+----+------------+--------+-------------+
|  5 | Bette      | Davis     | bette@aol.com    |  1 | 2016-02-10 |  99.99 |           1 |
|  4 | Blue       | Steele    | blue@gmail.com   |  1 | 2016-02-10 |  99.99 |           1 |
|  3 | David      | Bowie     | david@gmail.com  |  1 | 2016-02-10 |  99.99 |           1 |
|  2 | George     | Michael   | gm@gmail.com     |  1 | 2016-02-10 |  99.99 |           1 |
|  1 | Boy        | George    | george@gmail.com |  1 | 2016-02-10 |  99.99 |           1 |
|  5 | Bette      | Davis     | bette@aol.com    |  2 | 2017-11-11 |  35.50 |           1 |
|  4 | Blue       | Steele    | blue@gmail.com   |  2 | 2017-11-11 |  35.50 |           1 |
|  3 | David      | Bowie     | david@gmail.com  |  2 | 2017-11-11 |  35.50 |           1 |
|  2 | George     | Michael   | gm@gmail.com     |  2 | 2017-11-11 |  35.50 |           1 |
|  1 | Boy        | George    | george@gmail.com |  2 | 2017-11-11 |  35.50 |           1 |
|  5 | Bette      | Davis     | bette@aol.com    |  3 | 2014-12-12 | 800.67 |           2 |
|  4 | Blue       | Steele    | blue@gmail.com   |  3 | 2014-12-12 | 800.67 |           2 |
|  3 | David      | Bowie     | david@gmail.com  |  3 | 2014-12-12 | 800.67 |           2 |
|  2 | George     | Michael   | gm@gmail.com     |  3 | 2014-12-12 | 800.67 |           2 |
|  1 | Boy        | George    | george@gmail.com |  3 | 2014-12-12 | 800.67 |           2 |
|  5 | Bette      | Davis     | bette@aol.com    |  4 | 2015-01-03 |  12.50 |           2 |
|  4 | Blue       | Steele    | blue@gmail.com   |  4 | 2015-01-03 |  12.50 |           2 |
|  3 | David      | Bowie     | david@gmail.com  |  4 | 2015-01-03 |  12.50 |           2 |
|  2 | George     | Michael   | gm@gmail.com     |  4 | 2015-01-03 |  12.50 |           2 |
|  1 | Boy        | George    | george@gmail.com |  4 | 2015-01-03 |  12.50 |           2 |
|  5 | Bette      | Davis     | bette@aol.com    |  5 | 1999-04-11 | 450.25 |           5 |
|  4 | Blue       | Steele    | blue@gmail.com   |  5 | 1999-04-11 | 450.25 |           5 |
|  3 | David      | Bowie     | david@gmail.com  |  5 | 1999-04-11 | 450.25 |           5 |
|  2 | George     | Michael   | gm@gmail.com     |  5 | 1999-04-11 | 450.25 |           5 |
|  1 | Boy        | George    | george@gmail.com |  5 | 1999-04-11 | 450.25 |           5 |
+----+------------+-----------+------------------+----+------------+--------+-------------+
```


## INNER JOIN
```sql
SELECT * FROM customers JOIN orders ON customers.id = orders.customer_id;
+----+------------+-----------+------------------+----+------------+--------+-------------+
| id | first_name | last_name | email            | id | order_date | amount | customer_id |
+----+------------+-----------+------------------+----+------------+--------+-------------+
|  1 | Boy        | George    | george@gmail.com |  1 | 2016-02-10 |  99.99 |           1 |
|  1 | Boy        | George    | george@gmail.com |  2 | 2017-11-11 |  35.50 |           1 |
|  2 | George     | Michael   | gm@gmail.com     |  3 | 2014-12-12 | 800.67 |           2 |
|  2 | George     | Michael   | gm@gmail.com     |  4 | 2015-01-03 |  12.50 |           2 |
|  5 | Bette      | Davis     | bette@aol.com    |  5 | 1999-04-11 | 450.25 |           5 |
+----+------------+-----------+------------------+----+------------+--------+-------------+
```
INNER JOIN은 위와 같이 쿼리를 만들 수 있다.

```sql
mysql> SELECT first_name, last_name, order_date, amount FROM orders JOIN customers ON customers.id = orders.customer_id ORDER BY 4;
+------------+-----------+------------+--------+
| first_name | last_name | order_date | amount |
+------------+-----------+------------+--------+
| George     | Michael   | 2015-01-03 |  12.50 |
| Boy        | George    | 2017-11-11 |  35.50 |
| Boy        | George    | 2016-02-10 |  99.99 |
| Bette      | Davis     | 1999-04-11 | 450.25 |
| George     | Michael   | 2014-12-12 | 800.67 |
+------------+-----------+------------+--------+
```


아래가 된다는 게 신기하다
1. -- Our first inner join!
2. SELECT * FROM customers
3. JOIN orders ON orders.customer_id = customers.id;

5. SELECT first_name, last_name, order_date, amount FROM customers
6. JOIN orders ON orders.customer_id = customers.id;

8. -- The order doesn't matter here:
9. SELECT * FROM orders
10. JOIN customers ON customers.id = orders.customer_id;

## GROUP BY
```sql
mysql> SELECT first_name, last_name, SUM(amount) FROM customers JOIN orders ON orders.customer_id = customers.id GROUP BY first_name, last_name;
+------------+-----------+-------------+
| first_name | last_name | SUM(amount) |
+------------+-----------+-------------+
| Boy        | George    |      135.49 |
| George     | Michael   |      813.17 |
| Bette      | Davis     |      450.25 |
+------------+-----------+-------------+
```

orders에 first_name 없어서 customer.first_name으로 사용 안해도 됨.

```sql
SELECT first_name, last_name, SUM(amount) as total FROM customers
JOIN orders ON orders.customer_id = customers.id
GROUP BY first_name, last_name
ORDER BY total;
```

## LEFT JOIN

```sql
SELECT first_name, last_name, order_date, amount FROM customers
LEFT JOIN orders ON orders.customer_id = customers.id;
```

모든 customers가 나타나게 된다.

## RIGHT JOIN
```sql
SELECT 
    first_name, last_name, order_date, amount
FROM
    customers
        RIGHT JOIN
    orders ON customers.id = orders.customer_id;
```

### data insertion
```sql
CREATE TABLE customers(
	id INT PRIMARY KEY AUTO_INCREMENT,
	first_name VARCHAR(50),
	last_name VARCHAR(50),
	email VARCHAR(50)
);

CREATE TABLE orders(
	id INT PRIMARY KEY AUTO_INCREMENT,
	order_date DATE,
	amount DECIMAL(8,2),
	customer_id INT,
	FOREIGN KEY (customer_id) REFERENCES customers(id) ON DELETE CASCADE
);
```

## 예제
```sql
CREATE TABLE STUDENTS(
	id INT PRIMARY KEY AUTO_INCREMENT,
	first_name VARCHAR(100)
);

CREATE TABLE PAPERS(
	title VARCHAR(100),
	grade INT,
	student_id INT,
	FOREIGN KEY (student_id) REFERENCES STUDENTS(id) ON DELETE CASCADE
);
```

```sql
SELECT s.first_name, AVG(p.grade) as average FROM students s LEFT JOIN papers p ON p.student_id = s.id
GROUP BY s.first_name, p.grade;
```

여기서
> GROUP BY s.first_name, p.grade;

가 왜 필요한 걸까?

s.first_name만 해도 나옴

```sql
SELECT s.first_name, IFNULL(AVG(p.grade), 0) as average FROM students s LEFT JOIN papers p ON p.student_id = s.id
GROUP BY s.first_name, p.grade;
```

[[GROUP BY]]

```sql
SELECT s.first_name, CASE WHEN AVG(p.grade) is NULL THEN 0 END AS average FROM students s LEFT JOIN papers p ON p.student_id = s.id
GROUP BY s.first_name, p.grade;
```

```sql
SELECT s.first_name, 
	CASE 
		WHEN
			AVG(p.grade) is NULL THEN 0
			ELSE AVG(p.grade)
		END AS average
	FROM students s LEFT JOIN papers p ON p.student_id = s.id
GROUP BY s.first_name, p.grade;
```


### GROUP BY 주의해야 하는 이유
```sql
SELECT s.first_name, 
	CASE 
		WHEN
			AVG(p.grade) is NULL THEN 0
			ELSE AVG(p.grade)
		END AS average
	FROM students s LEFT JOIN papers p ON p.student_id = s.id
GROUP BY s.first_name
ORDER BY 2 DESC;
```


## subquery 쓰는 법
```sql
SELECT
	first_name, average,
	CASE 
		WHEN average>70 THEN "PASSING"
		ELSE "FAILING"
	END AS passing_status
FROM (SELECT 
		s.first_name, 
		CASE 
			WHEN AVG(p.grade) is NULL THEN 0
			ELSE AVG(p.grade)
		END AS average
	FROM students s
	LEFT JOIN papers p ON p.student_id = s.id
	GROUP BY s.first_name) AS subquery
ORDER BY 2 DESC;
```

LEFT JOIN이랑 GROUP BY 사이에 , 가 있으면 안 됨

# Many to Many
![[Screenshot 2024-05-30 at 19.13.09.png]]

