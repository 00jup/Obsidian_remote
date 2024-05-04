
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

## CURDATE, CURTIME 도 사용가능함
```sql
INSERT INTO people (name, birthdate, birthtime, birthdt) VALUES('Juan', CURDATE(), CURTIME(), '2020-08-15 23:59:00');
```

## NOW(), CURRENT_TIME()도 사용 가능하다!

## DATE_FORMAT()

```sql
mysql> SELECT birthdate, DATE_FORMAT(birthdate, '%a %b') FROM people;
+------------+---------------------------------+
| birthdate  | DATE_FORMAT(birthdate, '%a %b') |
+------------+---------------------------------+
| 2000-12-25 | Mon Dec                         |
| 1985-04-11 | Thu Apr                         |
| 2020-08-15 | Sat Aug                         |
| 2024-05-04 | Sat May                         |
| 2024-05-04 | Sat May                         |
+------------+---------------------------------+
```

```sql
mysql> SELECT DATE_FORMAT('2009-10-04 22:23:00', '%W %M %Y');
        -> 'Sunday October 2009'
mysql> SELECT DATE_FORMAT('2007-10-04 22:23:00', '%H:%i:%s');
        -> '22:23:00'
mysql> SELECT DATE_FORMAT('1900-10-04 22:23:00',
    ->                 '%D %y %a %d %m %b %j');
        -> '4th 00 Thu 04 10 Oct 277'
mysql> SELECT DATE_FORMAT('1997-10-04 22:23:00',
    ->                 '%H %k %I %r %T %S %w');
        -> '22 22 10 10:23:00 PM 22:23:00 00 6'
mysql> SELECT DATE_FORMAT('1999-01-01', '%X %V');
        -> '1998 52'
mysql> SELECT DATE_FORMAT('2006-06-00', '%d');
        -> '00'
```

TIME_FORMAT도 있음
근데 DATE_FORMAT support all of it.

# DATE 연산
```sql
mysql> SELECT name, birthdate, YEAR(birthdate + INTERVAL 21 YEAR) FROM people;
```

### INTERVAL을 사용해서 더 한다

# TIMESTAMP
DATETIME이랑 range가 다르다.
또 auto updating이 가능함
메모리 소모가 적다.

```sql
mysql> CREATE TABLE captions (
    -> text VARCHAR(150),
    -> created_at TIMESTAMP default CURRENT_TIMESTAMP);
```

이렇게 작성하는 게 가능함

```sql
CREATE TABLE captions2 (
    text VARCHAR(150),
    created_at TIMESTAMP default CURRENT_TIMESTAMP,
    updated_at TIMESTAMP ON UPDATE CURRENT_TIMESTAMP);
```

```sql
CREATE TABLE captions2 (
    text VARCHAR(150),
    created_at TIMESTAMP default CURRENT_TIMESTAMP,
    updated_at TIMESTAMP ON UPDATE CURRENT_TIMESTAMP);
```

위와 같이 작성하면 update 한 시간이 저장된다.

```sql
mysql> UPDATE captions2 SET text = 'i love live!!!';
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> SELECT * FROM captions2
    -> ;
+----------------+---------------------+---------------------+
| text           | created_at          | updated_at          |
+----------------+---------------------+---------------------+
| i love live!!! | 2024-05-04 17:58:09 | 2024-05-04 17:58:49 |
+----------------+---------------------+---------------------+
1 row in set (0.01 sec)
```

