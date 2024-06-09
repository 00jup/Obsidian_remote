

```java
PersonFactory personFactory = () -> { return new Person(); };
```

위에서 중괄호 없애면 아래와 같이 변경

```java
PersonFactory personFactory = () -> new Person();
```