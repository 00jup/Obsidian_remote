
## SQL에서 Single Quote와 Double Quote의 사용 규칙

### 문자열 리터럴 (String Literals)
- 문자열 리터럴은 반드시 single quote(')로 감싸야 한다.
- 예시:
  ```sql
  DELETE FROM boards WHERE bwriter = 'jup';
  ```

### 식별자 (Identifiers)
- 테이블명, 컬럼명 등 식별자를 감쌀 때는 double quote(")를 사용한다.
- 예시:
  ```sql
  SELECT "column_name" FROM "table_name";
  ```

### 예시를 통한 설명
- **잘못된 예시**: 문자열 리터럴에 double quote를 사용한 경우
  ```sql
  DELETE FROM boards WHERE bwriter = "jup";
  ```
  - 오류 메시지: `ORA-00904: "jup": invalid identifier`

- **올바른 예시**: 문자열 리터럴에 single quote를 사용한 경우
```sql
  DELETE FROM boards WHERE bwriter = 'jup';
```