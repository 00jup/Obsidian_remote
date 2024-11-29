![[Pasted image 20241129223253.png]]

주어진 예제에서 트리거의 실행 순서는 다음과 같다:

### **1. 트리거 우선순위 지정**
- `PRECEDES ins_sum` 문구에 따라, `ins_transaction` 트리거는 **`ins_sum` 트리거보다 먼저 실행**된다.
- MySQL에서는 동일한 이벤트(`BEFORE INSERT`)에 여러 트리거가 정의되어 있을 경우, `PRECEDES`와 `FOLLOWS` 키워드를 사용해 실행 순서를 지정할 수 있다.

### **2. 실행 순서**
- `BEFORE INSERT ON account` 작업이 실행될 때, MySQL은 먼저 `PRECEDES`로 정의된 `ins_transaction` 트리거를 실행한다.
- 이후 `ins_sum` 트리거가 실행된다.
- 실행 순서:
  1. `ins_transaction` 트리거 실행
     - 여기서 트리거 내부의 로직이 수행된다:
       ```sql
       @deposits = @deposits + IF(NEW.amount > 0, NEW.amount, 0);
       @withdrawals = @withdrawals + IF(NEW.amount < 0, -NEW.amount, 0);
       ```
     - 새로운 값이 `@deposits`와 `@withdrawals`에 반영된다.
  2. `ins_sum` 트리거 실행 (만약 `ins_sum`의 구현 내용이 있다면 실행된다)

---

### **3. 핵심**
- 트리거는 **명시적으로 정의된 순서(PRECEDES/FOLLOWS)**에 따라 실행된다.
- `ins_transaction` 트리거는 `ins_sum`보다 먼저 실행되며, 같은 `BEFORE INSERT` 이벤트 안에서도 우선순위를 가진다.
- `ins_sum` 트리거의 실제 동작 내용은 명시되지 않았으나, 순서상 `ins_transaction`이 먼저 실행되고 나중에 실행된다.

**MySQL의 `AFTER INSERT`, `PRECEDES`, 그리고 `FOLLOWS`**는 트리거 동작과 실행 순서를 정의하는 중요한 개념이다. 아래에서 각각을 설명한다:

---

### **1. `AFTER INSERT`**
- **설명**  
  - `AFTER INSERT` 트리거는 **INSERT 작업이 완료된 후** 실행된다.
  - 데이터가 테이블에 성공적으로 삽입된 다음에 실행되며, 데이터 변경 후 처리 작업에 적합하다.
  - 주로 **로깅**, **추가 데이터 계산**, 또는 **다른 테이블 갱신** 작업을 위해 사용된다.

- **구문**  
  ```sql
  CREATE TRIGGER trigger_name
  AFTER INSERT ON table_name
  FOR EACH ROW
  BEGIN
      -- 작업 수행
  END;
  ```

- **사용 예제**
  ```sql
  CREATE TRIGGER after_insert_log
  AFTER INSERT ON accounts
  FOR EACH ROW
  BEGIN
      -- 새로 삽입된 데이터를 로그 테이블에 기록
      INSERT INTO log_table (account_id, action, timestamp)
      VALUES (NEW.id, 'INSERT', NOW());
  END;
  ```
  - 위 트리거는 `accounts` 테이블에 데이터가 삽입된 후, `log_table`에 기록을 남긴다.

- **주요 특징**
  - `AFTER INSERT`는 작업 후 실행되기 때문에 삽입된 데이터가 반드시 테이블에 반영된다.
  - 트랜잭션이 `ROLLBACK`될 경우 트리거도 실행되지 않는다.

---

### **2. `PRECEDES`**
- **설명**  
  - 동일한 이벤트(예: `BEFORE INSERT`)에 여러 트리거가 정의된 경우, **실행 순서를 지정**하기 위해 사용된다.
  - `PRECEDES`는 특정 트리거가 다른 트리거보다 **먼저 실행**되도록 한다.

- **구문**
  ```sql
  CREATE TRIGGER trigger1
  BEFORE INSERT ON table_name
  FOR EACH ROW
  PRECEDES trigger2
  BEGIN
      -- 작업 수행
  END;
  ```

- **사용 예제**
  ```sql
  CREATE TRIGGER validate_data
  BEFORE INSERT ON accounts
  FOR EACH ROW
  PRECEDES log_insert;

  CREATE TRIGGER log_insert
  BEFORE INSERT ON accounts
  FOR EACH ROW
  BEGIN
      INSERT INTO log_table (account_id, action) VALUES (NEW.id, 'VALIDATION LOG');
  END;
  ```
  - 이 경우, `validate_data` 트리거가 먼저 실행되고, 그 다음에 `log_insert` 트리거가 실행된다.

- **주요 특징**
  - `PRECEDES`는 특정 트리거가 순서적으로 우선 실행되도록 지정한다.
  - 트리거 실행 순서를 명확히 하고자 할 때 유용하다.

---

### **3. `FOLLOWS`**
- **설명**  
  - `FOLLOWS`는 `PRECEDES`와 반대 동작으로, 특정 트리거가 **다른 트리거의 뒤에 실행**되도록 한다.
  - 트리거의 실행 순서를 명시적으로 설정할 수 있다.

- **구문**
  ```sql
  CREATE TRIGGER trigger2
  BEFORE INSERT ON table_name
  FOR EACH ROW
  FOLLOWS trigger1
  BEGIN
      -- 작업 수행
  END;
  ```

- **사용 예제**
  ```sql
  CREATE TRIGGER calculate_balance
  BEFORE INSERT ON accounts
  FOR EACH ROW
  FOLLOWS validate_data;

  CREATE TRIGGER validate_data
  BEFORE INSERT ON accounts
  FOR EACH ROW
  BEGIN
      IF NEW.balance < 0 THEN
          SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Balance cannot be negative';
      END IF;
  END;
  ```
  - 여기서 `validate_data` 트리거가 먼저 실행되어 데이터가 유효한지 확인한 후, `calculate_balance` 트리거가 실행된다.

- **주요 특징**
  - `FOLLOWS`는 특정 트리거가 나중에 실행되도록 한다.
  - 여러 트리거를 논리적 순서로 실행하고자 할 때 유용하다.

---

### **4. `PRECEDES`와 `FOLLOWS`의 동작 원리**
- MySQL은 **같은 이벤트**(예: `BEFORE INSERT` 또는 `AFTER INSERT`)에 여러 트리거가 정의되어 있으면, `PRECEDES`와 `FOLLOWS` 키워드를 통해 실행 순서를 결정한다.
- 기본적으로 MySQL은 트리거를 생성된 순서대로 실행한다. 하지만 `PRECEDES`와 `FOLLOWS`를 사용하면 명시적으로 순서를 지정할 수 있다.

---

### **정리**
- **`AFTER INSERT`**: 데이터가 테이블에 성공적으로 삽입된 후 트리거 실행.
- **`PRECEDES`**: 트리거 실행 순서를 지정하며, 특정 트리거가 다른 트리거보다 먼저 실행되도록 한다.
- **`FOLLOWS`**: 트리거 실행 순서를 지정하며, 특정 트리거가 다른 트리거 뒤에 실행되도록 한다.

트리거의 순서를 지정하면 복잡한 로직을 체계적으로 관리할 수 있으며, 데이터 무결성을 보장할 수 있다.