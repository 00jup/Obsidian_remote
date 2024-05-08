
```java
public class Test {
    public static void main(String args[]) {
        System.out.println("Provided String Arguments:");
        for(String i : args)
        {
            System.out.println(i);
        }      
    }    
}
```

여기서 void main 다음의 `String args[]` 가 나오는데 

terminal에서 만들어진 class 파일을 실행한다고 해보자

> java Test python java c

위와 같이 입력하면

>Provided String Arguments:
	Java
	Python
	Scala

위와 같은 결과를 얻을 수 있다.

[[String[] args VS String args[]의 차이점]]




