


`int step = steps[i];`
local class라서 final value로 초기화 되어야 함.
# Code
```java
package ch08.nestedPractice;

public class Counter {

    CalcElement[] calcarr = new CalcElement[3];
    private int count = 0;

    Counter(String[] optypes, int[] steps) {
        for(int i = 0; i< optypes.length; i++){
            calcarr[i] = new CalcElement();
            int step = steps[i];
            switch (optypes[i]){
                case "add":
                    calcarr[i].setOperator(new CalcElement.Operator() {
                        @Override
                        public int operate() {
                            return count + step;
                        }
                    });
                    break;
                case "mul":
                    calcarr[i].setOperator(new CalcElement.Operator() {
                        @Override
                        public int operate() {
                            return count * step;
                        }
                    });

                    break;
                case "sub":
                    calcarr[i].setOperator(new CalcElement.Operator() {
                        @Override
                        public int operate() {
                            return count - step;
                        }
                    });

                    break;
            }

        }
    }

    void showCount() {
        System.out.println("The number is " + count + " now.");
    }

    void clickButton(int n){
        count = calcarr[n].operate();
    }
}

```


```java
new CalcElement.Operator() {
                        @Override
                        public int operate() {
                            return count + step;
                        }
```

여기서 operate를 주입한다.

```java
public class MulCal {
    public static void main(String[] args) {
        Scanner scan = new Scanner(System.in);

        System.out.print("Choose integers ");
        int[] integers = new int[10];
        //final int[] integers = new int[10];
        //교수님은 이거 final로 함. const를 포인터에 붙이냐 star 옆이냐 뒤에냐에 따라서 달라지는 것처럼
        for (int i = 0; i < 10; i++)
            integers[i] = scan.nextInt();

        Thread thread_sum = new Thread() {
            //int sum_result = 0;

            // 밖에서 선언하면 final임
            @Override
            public void run() {
                try {
                    int sum_result = 0;
                    for (int j = 0; j < 10; j++) {
                        sum_result = sum_result + integers[j];
                        Thread.sleep(700);
                        System.out.println("current sum: " + sum_result);
                        if (Math.abs(sum_result) > 1000) {
                            throw new Exception("The addition result is too large");
                        }
                    }
                } catch (Exception e) {
                    System.out.println(e.getMessage());
                    e.printStackTrace();
                }
            }

        };
    }
}
```

>//int sum_result = 0;
>// 밖에서 선언하면 final임

