


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


