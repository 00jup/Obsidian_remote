

## ClassExample.java
```java
package ch04.sec01;

public class ClassExample {
    int field;
    public static void main(String[] args) {
        Calculator n1 = new Calculator("Blue");
        Calculator n2 = new Calculator("Red");
        System.out.println(n1.color);
        System.out.println(Calculator.number);
        Calculator.number = 10;
        System.out.println(n1.number);
        System.out.println(n2.number);
        System.out.println(Calculator.number);
        Calculator.number = 20;
        System.out.println(n1.number);
        System.out.println(n2.number);
        System.out.println(Calculator.number);

    }
}
```
