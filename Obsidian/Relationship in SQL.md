
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




