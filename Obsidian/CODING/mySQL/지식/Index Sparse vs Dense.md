MySQL에서는 InnoDB 엔진이 Primary Key를 기반으로 자동으로 관리한다:

Primary Key (Sparse Index) 예시:
```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,  -- 자동으로 sparse index 생성
    name VARCHAR(50)
);
```
- 데이터 페이지 단위로 인덱스 생성
- 각 페이지의 첫 번째 레코드만 인덱스에 저장

Secondary Index (Dense Index) 예시:
```sql
CREATE INDEX idx_name ON employees (name);
```
- 모든 레코드에 대해 인덱스 엔트리 생성
- 각 엔트리는 Primary Key를 참조

실제 동작을 EXPLAIN으로 확인:
```sql
EXPLAIN SELECT * FROM employees WHERE id = 100;
-- "type: ref" (sparse index 사용)

EXPLAIN SELECT * FROM employees WHERE name = 'John';
-- "type: ref" (dense index 사용)
```

주의: MySQL에서는 이를 자동으로 관리하므로 개발자가 dense/sparse를 직접 지정할 수는 없다