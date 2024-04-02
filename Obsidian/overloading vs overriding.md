
# overloading
add 함수를 생각하면 편하다.

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

# overriding