
JOIN 으로 만든 테이블을 view에서 업데이트 하거나 지울 수 없다.

VIEW에서 

```mysql
CREATE OR REPLACE VIEW ordered_series AS
SELECT * FROM series ORDER BY released_year DESC
```

## ALTER TABLE

```mysql
ALTER VIEW ordered_series AS
SELECT * FROM series ORDER BY released_year DESC
```

## HAVING
```mysql
SELECT
	title,
	AVG(rating)
FROM full_reviews
GROUP BY title HAVING COUNT(rating) > 1;
```

GROUP BY를 사용하면 HAVING을 사용하도록!



