`toString` 메서드를 재정의하면 다른 출력이 나오는 이유는 `toString` 메서드가 객체를 문자열로 표현하는 방법을 정의하기 때문이다. 기본적으로, `Object` 클래스의 `toString` 메서드는 객체의 클래스 이름과 해시코드를 반환하지만, 이를 재정의하면 우리가 원하는 형식의 문자열을 반환할 수 있다.

이것을 이해하기 위해, 기본 구현과 재정의한 구현의 차이를 자세히 살펴보자.

### 기본 구현

`Object` 클래스에 정의된 기본 `toString` 메서드는 다음과 같이 생겼다:

```java
public String toString() {
    return getClass().getName() + "@" + Integer.toHexString(hashCode());
}
```

이 메서드는 객체의 클래스 이름과 해시코드를 16진수로 반환한다.

### 재정의된 구현

`toString` 메서드를 재정의하여 객체의 상태를 포함한 문자열을 반환할 수 있다. 예를 들어, `Person` 클래스에서 다음과 같이 `toString` 메서드를 재정의할 수 있다:

```java
@Override
public String toString() {
    return "Person{name='" + name + "', age=" + age + "}";
}
```

이 재정의된 메서드는 `Person` 객체의 `name`과 `age` 필드를 포함하는 문자열을 반환한다.

### 동작 원리

Java에서 `System.out.println` 메서드는 인자로 전달된 객체의 `toString` 메서드를 호출하여 반환된 문자열을 출력한다. 따라서 `toString` 메서드를 재정의하면 `System.out.println`을 호출할 때 재정의된 `toString` 메서드가 호출되어 그 결과가 출력된다.

예를 들어:

```java
Person person = new Person("John", 25);
System.out.println(person);
```

이 코드는 내부적으로 `person.toString()`을 호출하여 그 결과를 출력한다. 만약 `toString` 메서드를 재정의하지 않았다면 기본 구현이 호출되어 클래스 이름과 해시코드가 출력되지만, 재정의된 경우에는 재정의한 내용이 출력된다.