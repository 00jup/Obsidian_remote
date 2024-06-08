```java
package weeks14.threadWaitNotify;

public class WorkObject {
    public synchronized void methodA() {
        Thread thread = Thread.currentThread();
        System.out.println(thread.getName() + ": methodA 작업 실행");
        try {
            wait(); // 다른 스레드에 의해 notify()가 호출될 때까지 대기
        } catch (InterruptedException e) {
            // 예외 처리
        }
        notifyAll(); // 대기 중인 스레드에게 신호를 보냄

    }

    public synchronized void methodB() {
        Thread thread = Thread.currentThread();
        System.out.println(thread.getName() + ": methodB 작업 실행");
        try {
            wait();
        } catch (InterruptedException e) {
            // 예외 처리
        }
        notifyAll();
    }
}
```

wait랑 notify 순서만 바꿨는데 왜 다르게 나올까.

wait()를 실행하면 thread가 대기 상태로 들어가서 그렇다!
