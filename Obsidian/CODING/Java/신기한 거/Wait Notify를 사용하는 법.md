# Wait와 Notify

Java에서 `wait()`와 `notify()`는 스레드 간의 작업 순서를 제어하는 데 사용되는 메서드입니다. 이들은 모니터링(monitoring) 개념과 밀접한 관련이 있습니다.

## wait()

`wait()` 메서드는 현재 스레드가 lock을 해제하고 다른 스레드에게 실행 기회를 넘기게 합니다. 이 메서드를 호출한 스레드는 다른 스레드에 의해 `notify()` 또는 `notifyAll()`이 호출될 때까지 대기 상태에 있게 됩니다.

- `wait()`는 반드시 동기화 블록 내에서 호출되어야 합니다. 그렇지 않으면 `IllegalMonitorStateException`이 발생합니다.
- `wait()`는 `InterruptedException`을 throw할 수 있으므로, 이를 적절히 처리해야 합니다.

```java
synchronized (obj) {
    try {
        obj.wait(); // 대기 상태로 들어감
    } catch (InterruptedException e) {
        // 예외 처리
    }
}
```

## notify()

`notify()` 메서드는 대기 중인 스레드 중 하나에게 신호를 보내 대기 상태에서 깨어나게 합니다. 이 메서드를 호출하면 해당 객체의 대기 중인 스레드 중 하나가 깨어나 lock을 획득하여 실행할 수 있게 됩니다.

- 만약 대기 중인 스레드가 없으면 `notify()`는 아무 효과가 없습니다.
- `notifyAll()`은 대기 중인 모든 스레드를 깨웁니다.

```java
synchronized (obj) {
    // 작업 수행
    obj.notify(); // 대기 중인 스레드 중 하나에게 신호 전달
}
```

## 활용 예시

`wait()`와 `notify()`는 주로 생산자-소비자 문제와 같은 스레드 동기화 상황에서 사용됩니다.

```java
public class WorkObject {
    public synchronized void methodA() {
        System.out.println(Thread.currentThread().getName() + ": methodA 작업 실행");
        notify(); // 대기 중인 스레드에게 신호 보냄

        try {
            wait(); // 다른 스레드에 의해 notify()가 호출될 때까지 대기
        } catch (InterruptedException e) {
            // 예외 처리
        }
    }

    public synchronized void methodB() {
        System.out.println(Thread.currentThread().getName() + ": methodB 작업 실행");
        notify();

        try {
            wait();
        } catch (InterruptedException e) {
            // 예외 처리
        }
    }
}
```

이 예시에서 `methodA()`와 `methodB()`는 `synchronized` 키워드로 동기화되어 있습니다. 한 스레드가 `methodA()`를 실행하면 `notify()`를 호출하여 대기 중인 다른 스레드에게 신호를 보내고, `wait()`를 호출하여 대기 상태로 들어갑니다. 이때 다른 스레드가 깨어나 `methodB()`를 실행하게 됩니다. 이렇게 번갈아가며 작업을 실행하면서 스레드 간 작업 순서를 제어할 수 있습니다.

## 주의사항

- `wait()`와 `notify()`는 항상 동기화 블록 내에서 호출되어야 합니다. 그렇지 않으면 예외가 발생합니다.
- `wait()`는 `InterruptedException`을 throw할 수 있으므로, 반드시 예외 처리를 해야 합니다.
- `notify()`를 호출해도 깨어난 스레드가 바로 실행되는 것은 아닙니다. 스레드 스케줄러에 의해 실행 순서가 결정됩니다.
- `notifyAll()`을 사용하면 모든 대기 중인 스레드가 깨어나므로, 작업 순서 제어에 주의해야 합니다.