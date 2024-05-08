
어떤 의미이지 생각하다가, python에서의 class 변수와 의미가 비슷하다는 점을 알게되었다.

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

> 여기서 number라는 변수는 class 변수로 사용되고 있다.
## Calculator.java
```java
package ch04.sec01;

public class Calculator {

    public static int number;

    final String color;
    // 반드시 초기화는 한번 해줘야 한다.
    final static double pi;
    // 이렇게 상수로 쓸 거면 대문자로 지정함. PI
    static double inverse_pi;
    // 틀 안에 변수가 들어있는 거임.
    // pi라는 값은 객체 안에 있는 계속 똑같은 값으로 초기화시키는 게 비효율적이다.
    // pi = 3.14 비효율적이라는 거임
    // pi는 Calculator만의 속성이니까 정적 필드라고 말할 수 있다.
    // -> static double pi

    static {
        pi = 3.14;
        // 객체가 생성되기 전에 이 코드가 실행이 되어서 초기화 된다.
        inverse_pi = 1/pi;
        // 위에서 초기화하면서 하면 누가 먼저 실행될지 몰라서 복잡할 수 있다.
        // 여기 color = "Black"과 같이 객체에 소속된 걸 초기화할 수 없다.
        // 객체가 생성되기 전에 만들어짐
    }

    Calculator(String color){
        this.color = color;
        // 정적필드 constructor 안에서 초기화하는 건 살짝 부자연스럽다.
        // 그래서 객체가 생성되기 전에 초기화 해야 함.
        // static block 사용 가능하다.
    }

    void setColor(String color){
        // this.color = color;
        // final로 하면 위에서 오류가 남
    }

    static int plus(int x, int y){
        Calculator cal = new Calculator("Black");
        // cal.color = "white";
        // final로 하면 위에서 오류가 남

        // 만약에 사용하고 싶다면 이렇게 객체를 만들고 사용하기
        return x+y;
        // 여기 안에 this.color 사용하는 건 불가능하다.
        // 여기서 사용하고 싶다면 객체를 만들어야 함.
    }
    // 객체에  종속되어 있는 method가 아니다.
}
```
