## 1번 방법

```java
public class StringExample {
    public static void main(String[] args) {
        // Declare and initialize a string array
        String[] A = new String[2];

        // Set elements
        A[0] = "Hello";
        A[1] = "World";

        // Access and print elements
        System.out.println(A[0] + " " + A[1]);
    }
}
```

## 2번 방법

```java
public class StringExample {
    public static void main(String[] args) {
        // Declare and initialize a string array
        String[] A;

        // Set elements
        A = new String[] {"Hello", "World"};

        // Access and print elements
        System.out.println(A[0] + " " + A[1]);
    }
}
```