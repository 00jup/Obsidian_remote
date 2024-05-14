
`Function` 인터페이스의 `apply` 메서드는 다양한 상황에서 사용될 수 있습니다. 몇 가지 예시를 더 살펴보겠습니다.

1. 문자열 변환하기:
```java
Function<String, String> upperCaseFunction = s -> s.toUpperCase();
String result = upperCaseFunction.apply("hello, world!");
System.out.println(result); // 출력: "HELLO, WORLD!"
```
이 예시에서는 `Function<String, String>`을 사용하여 문자열을 대문자로 변환하는 함수를 정의합니다. 람다 표현식 `s -> s.toUpperCase()`는 입력 문자열 `s`를 받아 `toUpperCase()` 메서드를 호출하여 대문자로 변환된 문자열을 반환합니다.

2. 숫자 범위 확인하기:
```java
Function<Integer, Boolean> isPositiveFunction = num -> num > 0;
boolean isPositive = isPositiveFunction.apply(-5);
System.out.println(isPositive); // 출력: false
```
이 예시에서는 `Function<Integer, Boolean>`을 사용하여 숫자가 양수인지 확인하는 함수를 정의합니다. 람다 표현식 `num -> num > 0`은 입력 숫자 `num`이 0보다 큰지 확인하여 그 결과를 boolean 값으로 반환합니다.

3. 객체 속성 추출하기:
```java
class Person {
    private String name;
    private int age;
    
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    public String getName() {
        return name;
    }
    
    public int getAge() {
        return age;
    }
}

Function<Person, String> getNameFunction = person -> person.getName();
String name = getNameFunction.apply(new Person("Alice", 25));
System.out.println(name); // 출력: "Alice"
```
이 예시에서는 `Function<Person, String>`을 사용하여 `Person` 객체에서 이름을 추출하는 함수를 정의합니다. 람다 표현식 `person -> person.getName()`은 입력 `Person` 객체 `person`에서 `getName()` 메서드를 호출하여 이름을 반환합니다.

4. 리스트 요소 필터링하기:
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
Function<Integer, Boolean> isEvenFunction = num -> num % 2 == 0;
List<Integer> evenNumbers = numbers.stream()
                                    .filter(isEvenFunction::apply)
                                    .collect(Collectors.toList());
System.out.println(evenNumbers); // 출력: [2, 4, 6, 8, 10]
```
이 예시에서는 `Function<Integer, Boolean>`을 사용하여 숫자가 짝수인지 확인하는 함수를 정의합니다. 람다 표현식 `num -> num % 2 == 0`은 입력 숫자 `num`이 2로 나누어 떨어지는지 확인하여 그 결과를 boolean 값으로 반환합니다. 그런 다음 `filter` 메서드에 `isEvenFunction::apply`를 전달하여 리스트에서 짝수만 필터링합니다.

이처럼 `Function` 인터페이스의 `apply` 메서드는 다양한 상황에서 사용될 수 있으며, 입력값을 받아 원하는 결과를 반환하는 함수를 정의할 때 유용하게 활용할 수 있습니다.