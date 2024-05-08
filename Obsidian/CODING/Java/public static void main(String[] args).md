
```java
public class typecasting {
        int intValue = 10;
        byte byteValue = (byte) intValue;

        System.out.println(byteValue);
        System.out.println(intValue);

}
```

위 코드에서 static void main을 추가해줘야 한다.

안 그러면 어디서 시작하는지 모름.

```java
public class typecasting {
    public static void main(String[] args) {
        int intValue = 10;
        byte byteValue = (byte) intValue;

        System.out.println(byteValue);
        System.out.println(intValue);
    }

}
```