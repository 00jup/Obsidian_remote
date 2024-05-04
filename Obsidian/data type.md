
# CHAR vs VARCHAR
similliar but different
VARCHAR(10)일 때, 10이하를 입력할 수 있지만
CHAR has `fixed length`

char2일 때 'X'를 INSERT하면 white space가 자동으로 생김.
![[Screenshot 2024-05-04 at 15.08.30.png]]

## CHAR 유용할 때
![[Screenshot 2024-05-04 at 15.10.22.png]]

CHAR -> 이럴 때 유용함.
Otherwise, USE VARCHAR!!!

# INT
int의 유형 별로 byte가 달라짐.

양수만 입력하고 싶으면 table을 만들 때, UNSIGNED를 붙이면 된다.

# DECIMAL
![[Screenshot 2024-05-04 at 15.22.12.png]]
소수를 저장하고 싶을 때 사용한다.

float이랑은 뭐가 다를까?
![[Screenshot 2024-05-04 at 15.27.32.png]]

# DATETIME
date와 time을 동시에 사용하고 싶을 때 사용함.
```sql
mysql> INSERT INTO people (name, birthdate, birthtime, birthdt) VALUES('Lulu', '1985-04-11', '9:45:10',
'1985-04-11 9:45:10');

mysql> INSERT INTO people (name, birthdate, birthtime, birthdt) VALUES('Juan', '2020-08-15', '23:59:00', '2020-08-15 23:59:00');
```
