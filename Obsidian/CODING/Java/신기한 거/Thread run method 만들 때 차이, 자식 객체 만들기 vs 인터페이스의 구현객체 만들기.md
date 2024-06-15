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
Thread의 익명자식객체를 만드는 거고

## 익명 자식 객체 예시
```java
class Example{
	Tire tire1 = new Tire(){
		@Override
		public void run(){
			System.out.println("익명 자식 객체 타이어가 굴러갑니다.");
		}
	}
}
```

이거 자체로 익명 자식 객체가 되는 거다.



```java
package weeks16;

public class Thread1 extends Thread {
    public Thread1(Runnable target) {
        super(target);
    }

    @Override
    public void run() {
        System.out.println("thread 1");
    }
}

public class ThreadTest {
    public static void main(String[] args) {
        Thread1 thread1 = new Thread1(() -> {
            System.out.println("Hello");
        });
        thread1.start();
    }
}

```

Thread1에서 Runnable을 바로 던지려면 구현할 때 부모의 Runnable처럼 사용하기 위해서 위와 같이 구현해야 한다.