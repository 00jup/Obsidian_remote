```java
public class Main{
	 public static void main(String[] args){
		 Thread thread = new Thread(A)
	 }
}
```

A에서 new Runnable(){}하고 만드는 거랑

인터페이스의 구현객체를 만드는 거임

```java
public class Main{
	 public static void main(String[] args){
		 Thread thread = new Thread(){B}
	 }
}
```

B에서 @Override 해서 run method를 만드는 것의 차이
Thread의 자식객체를 만드는 거고