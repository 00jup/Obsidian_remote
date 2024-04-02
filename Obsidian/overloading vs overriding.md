
# overloading
add 함수를 생각하면 편하다.
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

# overriding
