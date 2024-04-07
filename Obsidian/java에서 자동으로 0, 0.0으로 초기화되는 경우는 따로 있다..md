## Java 변수 초기화 요약

### 자동 초기화되는 변수

- **클래스 레벨 변수**:
  - 인스턴스 변수와 클래스 변수(static 변수)는 기본값으로 자동 초기화된다.
- **기본값**:
  - 정수형(`byte`, `short`, `int`, `long`): `0`
  - 부동 소수점(`float`, `double`): `0.0`
  - 문자(`char`): `'\u0000'` (null 문자)
  - 불리언(`boolean`): `false`
  - 객체 참조(`String`, 배열 등): `null`

### 명시적 초기화가 필요한 변수

- **지역 변수**:
  - 메소드 내에서 선언된 변수는 자동 초기화되지 않는다.
  - 사용하기 전에 명시적으로 초기화해야 한다.

### 예시 코드

```java
public class AutoInitializationExample {
    // 인스턴스 변수
    private int number;
    private boolean isValid;
    private char character;
    private String text;
    
    // 클래스 변수 (static 변수)
    private static double classLevelDouble;

    public static void main(String[] args) {
        AutoInitializationExample example = new AutoInitializationExample();
        
        // 인스턴스 변수와 클래스 변수의 초기값 출력
        System.out.println("Number (int): " + example.number); // 0
        System.out.println("isValid (boolean): " + example.isValid); // false
        System.out.println("Character (char): " + example.character); // '\u0000' (null 문자)
        System.out.println("Text (String): " + example.text); // null
        System.out.println("Class level double: " + AutoInitializationExample.classLevelDouble); // 0.0
    }
}
```

이 예시는 클래스 레벨 변수가 자동으로 어떻게 초기화되는지 보여준다. 반면, 지역 변수는 이와 같은 자동 초기화를 받지 않으므로, 사용 전에 반드시 초기화해야 한다.