1. 제네릭(Generic)은 결정되지 않은 타입을 파라미터로 처리하고 실제 사용할 때 파라미터를 구체적인 타입으로 대체시키는 기능입니다.

예시 코드:
```java
public class Box<T> {
    public T content;
}
```

2. 타입의 필요한 자리에 T를 사용할 수 있음을 알려줍니다. Box 객체가 생성될 시점에 다른 타입으로 대체됩니다.

3. T 자리에는 어떤 알파벳이든 가능합니다. 클래스 및 인터페이스가 올 수 있습니다.

실제 사용 예시:
```java
Box<String> box = new Box<String>();
box.content = "안녕하세요.";
String content = box.content;
```
```java
Box<Integer> box = new Box<Integer>();
box.content = 100;
int content = box.content;
```

위의 사진은 제네릭의 개념과 사용법을 설명하고 있습니다. 제네릭을 통해 클래스나 메소드에서 사용할 타입을 파라미터로 받아 유연하게 처리할 수 있습니다. 실제 사용 시점에 구체적인 타입으로 대체되어 타입 안정성을 제공합니다.