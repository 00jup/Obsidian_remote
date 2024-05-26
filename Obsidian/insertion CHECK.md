

```sql
CREATE TABLE partiers (
	name VARCHAR(50),
	age INT CHECK (age > 18)
);
```

```sql
CREATE TABLE partiers (
	name VARCHAR(50),
	age INT CHECK (REVERSE(word) = word)
);
```


SELECT REVERSE('hello');