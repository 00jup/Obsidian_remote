MySQL에서 Primary/Secondary Index 사용 예시:

Primary Index (Clustered Index)
```sql
-- 자동으로 clustered index가 생성되는 경우
CREATE TABLE students (
    student_id INT PRIMARY KEY,  -- InnoDB에서 자동으로 clustered index 생성
    name VARCHAR(50),
    major VARCHAR(50)
);

-- 명시적으로 clustered index 지정
CREATE TABLE courses (
    course_id INT,
    title VARCHAR(100),
    professor VARCHAR(50),
    PRIMARY KEY (course_id)  -- clustered index
);
```

Secondary Index
```sql
-- 단일 컬럼 secondary index
CREATE INDEX idx_student_name 
ON students (name);

-- 복합 컬럼 secondary index
CREATE INDEX idx_major_name 
ON students (major, name);

-- UNIQUE secondary index
CREATE UNIQUE INDEX idx_student_email 
ON students (email);
```

MySQL InnoDB에서는 PRIMARY KEY가 자동으로 clustered index가 되고, 다른 모든 인덱스는 secondary index가 된다

SI (Secondary Index)를 사용하지 않고 SELECT만 사용할 때의 차이를 설명하면:

인덱스가 없는 경우:
```sql
SELECT * FROM students WHERE name = '김철수';
```
- 전체 테이블을 처음부터 끝까지 스캔 (Table Full Scan)
- 데이터가 100만건이면 100만건을 모두 확인
- 시간복잡도: O(n)

Secondary Index 사용:
```sql
CREATE INDEX idx_name ON students (name);
SELECT * FROM students WHERE name = '김철수';
```
- 인덱스를 통해 바로 데이터 위치 접근
- B-tree 구조로 빠른 검색 가능
- 시간복잡도: O(log n)

예시로 보면:
- 100만건 데이터에서 특정 이름 찾기
  - 인덱스 없음: 최대 100만번 검색
  - 인덱스 있음: 약 20번의 검색으로 찾기 가능

다만 INSERT/UPDATE 시 인덱스도 함께 수정해야 해서 성능 저하가 있으므로, 자주 조회하는 컬럼에만 인덱스를 생성해야 한다