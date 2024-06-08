
```java
    public ThreadB(WorkObject workObject) {
        setName("ThreadB");
        this.workObject = workObject;
    }
```

실제 thread 내부에서는 thread.setName("ThreadB")가 아니라 그냥 바로 setName("ThreadB")가 사용이 가능하다.


```java
package weeks14.threadWaitNotify;
public class ThreadB extends Thread {
    private WorkObject workObject;

    public ThreadB(WorkObject workObject) {
        setName("ThreadB");
        this.workObject = workObject;
    }

    @Override
    public void run() {
        for(int i=0; i<10; i++) {
            workObject.methodB();
        }
    }
}
```

전체 코드는 위와 같다.ㅒ