Leading Column과 Trailing Column의 구분:

복합 인덱스에서 위치로 구분:
```sql
CREATE INDEX idx_name ON table (col1, col2, col3);
```
- Leading: col1 (첫번째 컬럼)
- Trailing: col2, col3 (그 뒤 컬럼들)

활용 차이:
```sql
-- Leading Column 활용 (인덱스 사용)
WHERE col1 = 'value'
WHERE col1 = 'value' AND col2 = 'value'

-- Trailing Column만 사용 (인덱스 사용 못함)
WHERE col2 = 'value'
WHERE col3 = 'value'

-- Leading Column 범위검색 후 Trailing (인덱스 일부 사용)
WHERE col1 > 'value' AND col2 = 'value'
```

순서가 중요한 이유:
- Leading Column이 없는 조건은 인덱스를 타지 못함
- Leading Column의 범위검색 이후 Trailing Column은 정렬된 상태를 활용할 수 없음