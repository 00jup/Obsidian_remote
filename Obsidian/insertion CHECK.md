

```sql
CREATE TABLE partiers (
	name VARCHAR(50),
	age INT CHECK (age > 18)
);
```

```sql
CREATE TABLE palindromes (
	word VARCHAR(100),
	CONSTRAINT parlindromes_chk_1 INT CHECK (REVERSE(word) = word)
);
```

REVERSE(word) = word
> boolean을 반환한다

SELECT REVERSE('hello');


```sql
Database changed
mysql> CREATE TABLE partiers2(   name VARCHAR(50), age INT, CONSTRAINT age_over_18 CHECK (age > 18) );
Query OK, 0 rows affected (0.04 sec)

mysql> INSERT INTO partiers2 (name, age)
    -> VALUES('chickne', -9);
ERROR 3819 (HY000): Check constraint 'age_over_18' is violated.
```

근데 constraint를 이렇게 따로 만드는 게 오류를 찾기 쉽다.