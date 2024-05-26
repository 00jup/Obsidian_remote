
```sql
CREATE TABLE companies(
	name VARCHAR(255) NOT NULL,
	address VARCHAR(255) NOT NULL,
	CONSTRAINT name_address UNIQUE (name, address)
)
```

unique이지 check를 쓰는 건 아니다


```sql
CREATE TABLE companies(
	name VARCHAR(255) NOT NULL,
	address VARCHAR(255) NOT NULL,
	CONSTRAINT name_address UNIQUE (name, address)
)
```

```sql
```