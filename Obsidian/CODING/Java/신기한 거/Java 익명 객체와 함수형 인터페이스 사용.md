
# Function.java
```java
package ch09.lambdaPractice;  
  
@FunctionalInterface  
public interface Function<T> {  
    public double apply(T t);  
}
```

# Example.java
```java
package ch09.lambdaPractice;

public class Example {
	private static Student[] students = {
		new Student("Mike", 90, 96),
		new Student("Maria", 94, 92)
	};
	
	public static double avg(Function<Student> function){
		int sum = 0;
		for(Student student:students){
			sum += function.apply(student);
		}
		return sum/students.length;

	}
	
	public static void main(String[] args) {
		double englishAvg = avg(Student::getEnglishScore); // 메소드 참조로 수정
		System.out.println("English average: " + englishAvg);
		
		double mathAvg = avg(Student::getMathScore); // 메소드 참조로 수정
		System.out.println("Math average: " + mathAvg);
	}

}
```

# Student.java
```java
package ch09.lambdaPractice;

public class Student {
	private String name;
	private double englishScore;
	private double mathScore;
	
	public Student(String name, double englishScore, double mathScore) {
		this.name = name;
		this.englishScore = englishScore;
		this.mathScore = mathScore;
	}
	
	public String getName() { return name; }
	public double getEnglishScore() { return englishScore; }
	public double getMathScore() { return mathScore; }

}
```

## Example.java에서
```java
public static double avg(Function<Student> function){
		int sum = 0;
		for(Student student:students){
			sum += function.apply(student);
		}
		return sum/students.length;

	}
```

왜 이게 function.apply(student)가 사용되는지 이해가 되지 않았다.

근데 아래 main 함수를 살펴보고 바로 이해할 수 있었다.

```java
public static void main(String[] args) {
		double englishAvg = avg(Student::getEnglishScore); // 메소드 참조로 수정
		System.out.println("English average: " + englishAvg);
		
		double mathAvg = avg(Student::getMathScore); // 메소드 참조로 수정
		System.out.println("Math average: " + mathAvg);
	}
```

위의 메소드 참조는 아래와 같이 바꿀 수 있다.

```java
public static void main(String[] args) {
		double englishAvg = avg(s -> s.getEnglishScore); // 메소드 참조로 수정
		System.out.println("English average: " + englishAvg);
		
		double mathAvg = avg(s -> s.getMathScore); // 메소드 참조로 수정
		System.out.println("Math average: " + mathAvg);
	}
```

위의 익명 객체는 아래와 같이 수정할 수 있다.

```java
public static void main(String[] args) {
		double englishAvg = avg(new Function<Student>() {  
                      @Override  
                      public double apply(Student student) {  
                         return student.getEnglishScore();  
                      }  
                   });  
System.out.println("English average: " + englishAvg);
		
		double englishAvg = avg(new Function<Student>() {  
                      @Override  
                      public double apply(Student student) {  
                         return student.getMathScore();  
                      }  
                   });  
System.out.println("English average: " + mathAvg);
	}
```

`이걸 보면 이제 납득이 된다...!`

[[Functional Interface Application]]

### 혼자 공부하다가 나온 오류
```java
double englishAvg = avg(
				()->{
					@Override
							public double apply(Student){
						return student.getEnglishScore();
					}
				}
				); // 메소드 참조로 수정
```