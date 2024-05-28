
```java
public static void main(String[] args){
        Scanner scan = new Scanner(System.in);

		int sum_result = 0;
        Thread thread_sum = new Thread(){
	        sum_result += 1;
        }
```
sum_result를 이렇게 사용하면 error가 나오는데, local variable을 local class에서 사용했기 때문이다.



```java
public static void main(String[] args){
        Scanner scan = new Scanner(System.in);

        Thread thread_sum = new Thread(){
            int sum_result = 0;
            // 밖에서 선언하면 final임
        }
```


