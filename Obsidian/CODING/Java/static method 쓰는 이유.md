

혼자 overload 공부하다가 알게 된 사실인데

```java
package ch06.sec02.test01;

public class AddExample {

    public static int add(int a, int b){
        return a+b;
    }
    public static double add(double a, double b){
        return a+b;
    }
    public static void main(String[] args){
        
        System.out.println(add(5,10));
        System.out.println(add(5.0,10.0));
    }
}
```

여기서 static method를 쓰면 객체를 생성하지 않고도 사용이 가능하다.

원래 코드는 아래와 같다.

```java
public int add(int a, int b){
        return a+b;
    }
    public double add(double a, double b){
        return a+b;
    }
    public static void main(String[] args){
        MainExample main = new MainExample();
        System.out.println(main.add(5,10));
        System.out.println(main.add(5.0,10.0));
    }
```