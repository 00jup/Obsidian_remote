`NEW`와 `OLD`는 MySQL 트리거 내에서 각각 **새로운 값**과 **기존 값**을 나타내며, 트리거가 처리하는 데이터의 상태를 구분하기 위해 사용된다. 이 두 개념은 트리거가 실행되는 이벤트(`INSERT`, `UPDATE`, `DELETE`)에 따라 다르게 동작한다.

---

### **1. `NEW`와 `OLD`의 기본 구분**

- **`NEW`**
  - **새로운 값**: 트리거 실행 중 삽입되거나 수정되는 데이터를 나타냄.
  - 사용 가능한 이벤트:
    - `INSERT`: 삽입될 데이터를 참조.
    - `UPDATE`: 업데이트 후의 데이터를 참조.

- **`OLD`**
  - **기존 값**: 트리거 실행 전에 이미 테이블에 존재하는 데이터를 나타냄.
  - 사용 가능한 이벤트:
    - `DELETE`: 삭제될 데이터를 참조.
    - `UPDATE`: 업데이트 전의 데이터를 참조.

---

### **2. 이벤트별 `NEW`와 `OLD` 동작**

| 이벤트          | `NEW` 사용 여부 | `OLD` 사용 여부 | 설명                                     |
|-----------------|----------------|----------------|----------------------------------------|
| **`INSERT`**    | 사용 가능       | 사용 불가       | 새로운 데이터가 삽입될 값을 참조.         |
| **`UPDATE`**    | 사용 가능       | 사용 가능       | `NEW`: 업데이트 후 값, `OLD`: 업데이트 전 값. |
| **`DELETE`**    | 사용 불가       | 사용 가능       | 삭제될 데이터를 참조.                     |

---

### **3. 사용 예시**

#### **(1) `INSERT` 이벤트**
```sql
CREATE TRIGGER after_insert_example
AFTER INSERT ON accounts
FOR EACH ROW
BEGIN
    -- NEW 값을 사용하여 로깅
    INSERT INTO log_table (account_id, balance)
    VALUES (NEW.id, NEW.balance);
END;
```
- `NEW.id`: 새로 삽입되는 `id` 값.
- `NEW.balance`: 새로 삽입되는 `balance` 값.

---

#### **(2) `UPDATE` 이벤트**
```sql
CREATE TRIGGER before_update_example
BEFORE UPDATE ON accounts
FOR EACH ROW
BEGIN
    -- 기존 값과 새로운 값 비교
    IF OLD.balance != NEW.balance THEN
        INSERT INTO log_table (account_id, old_balance, new_balance)
        VALUES (OLD.id, OLD.balance, NEW.balance);
    END IF;
END;
```
- `OLD.balance`: 기존 값(업데이트 전 값).
- `NEW.balance`: 업데이트 후 값.

---

#### **(3) `DELETE` 이벤트**
```sql
CREATE TRIGGER before_delete_example
BEFORE DELETE ON accounts
FOR EACH ROW
BEGIN
    -- 삭제될 데이터 기록
    INSERT INTO log_table (account_id, balance)
    VALUES (OLD.id, OLD.balance);
END;
```
- `OLD.id`: 삭제될 행의 `id` 값.
- `OLD.balance`: 삭제될 행의 `balance` 값.

---

### **4. 주요 차이점**
| 구분               | `NEW`          | `OLD`          |
| ---------------- | -------------- | -------------- |
| **삽입(INSERT)**   | 삽입될 데이터를 참조    | 사용 불가          |
| **업데이트(UPDATE)** | 업데이트 후 데이터를 참조 | 업데이트 전 데이터를 참조 |
| **삭제(DELETE)**   | 사용 불가          | 삭제될 데이터를 참조    |

---

### **5. 주의사항**
- **이벤트와의 연관성**
  - `NEW`와 `OLD`는 특정 이벤트에서만 사용할 수 있다. 예를 들어, `INSERT`에서는 `OLD`를 사용할 수 없다.
- **읽기 전용/수정 가능**
  - **`NEW`**: `BEFORE` 트리거에서는 값을 변경할 수 있다.
    ```sql
    SET NEW.amount = 0; -- BEFORE UPDATE에서 가능
    ```
  - **`OLD`**: 항상 읽기 전용이다. 값을 수정할 수 없다.
    ```sql
    SET OLD.amount = 0; -- 오류 발생
    ```

---

### **요약**
- **`NEW`**: 삽입 또는 업데이트 후의 데이터를 참조. `BEFORE` 트리거에서 수정 가능.
- **`OLD`**: 삭제되거나 업데이트 전의 데이터를 참조. 읽기 전용.
- 트리거의 이벤트(`INSERT`, `UPDATE`, `DELETE`)에 따라 사용 가능한 상태가 달라진다.