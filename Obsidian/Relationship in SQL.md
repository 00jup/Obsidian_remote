
1. one to one
![[Screenshot 2024-05-27 at 00.24.09 1.png]]


2.  one to many
![[Screenshot 2024-05-27 at 00.24.14.png]]


3.  many to many!
![[Screenshot 2024-05-27 at 00.24.17 1.png]]

## One to many Example
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
	amout DECIMAL(8,2),
	customer_id INT
);
```

이렇게 해도 작동에는 이상없음.

1. INSERT INTO customers (first_name, last_name, email)
2. VALUES ('Boy', 'George', 'george@gmail.com'),
3. ('George', 'Michael', 'gm@gmail.com'),
4. ('David', 'Bowie', 'david@gmail.com'),
5. ('Blue', 'Steele', 'blue@gmail.com'),
6. ('Bette', 'Davis', 'bette@aol.com');

INSERT INTO orders (order_date, amount, customer_id)
VALUES ('2016-02-10', 99.99, 1),
('2017-11-11', 35.50, 1),
('2014-12-12', 800.67, 2),('2015-01-03', 12.50, 2),('1999-04-11', 450.25, 5);