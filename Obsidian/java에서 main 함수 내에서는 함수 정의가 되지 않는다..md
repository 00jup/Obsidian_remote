
오류가 난 코드

```java
public class overloadingExample{
	
	public static void main(String[] args){
		int add(int A, int B){
			return A+B;
		}
		double add(double A, double B){
			return A+B;
		}
		System.out.println(add(5, 10));
		System.out.println(add(5.0, 10.0));
	}
	
}

```

java에서는 다른 언어처럼 함수를 위와 같이 사용할 수 없다.

아래와 같이 사용하면 할 수는 있음

```java
public class MainExample{
	public int add(int a, int b){
		return a+b;
	}
	public double add(double a, double b){
		return a+b;
	}
	public static void main(String[] args){
		MainExample main = new MainExample();
		System.out.println(main.add(5,10));
		System.out.println(main.add(5.0,10.0));
	}
}
```

