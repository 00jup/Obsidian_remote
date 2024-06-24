
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

