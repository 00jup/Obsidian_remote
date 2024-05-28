```java
package weeks13.ch14;

public class thread_example {
    public static void  main(String[] args){

        Thread thread1 = new Thread(new Runnable() {
            @Override
            public void run() {
                for (int i = 0; i< 5; i++){
                    System.out.println("작업 thread" + i);
                    try{Thread.sleep(500);}catch(Exception e){}
                }
            }
        });

        thread1.start();

        for (int j = 0; j<5; j++){
            System.out.println("Main thread"+j);
                    try{Thread.sleep(500);}catch(Exception e){}
        }

    }

}
```

병렬처리 되는 것을 확인할 수 있다. main이 먼저 종료되어도 프로그램이 종료되지 않는다.