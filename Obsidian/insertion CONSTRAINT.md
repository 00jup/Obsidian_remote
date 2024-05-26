
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
CREATE TABLE houses(
	purchase_price INT NOT NULL,
	sale_price INT NOT NULL,
	CONSTRAINT sprice_gt_pprice CHECK(sale_price >= purchase_price)
)
```

