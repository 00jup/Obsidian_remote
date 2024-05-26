
```sql
CRETE TABLE contacts(
	name VARCHAR(100) NOT NULL,
	phone VARCHAR(15) NOT NULL UNIQUE
)

INSERTION INTO contacts(name, phone)
VALUES('billybob', '8888888');

INSERTION INTO contacts(name, phone)
VALUES('ddd', '8888888');
-- 이러면 error남!
```

