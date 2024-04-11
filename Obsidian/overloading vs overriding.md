
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
부모 class에 있는 게 자식에도 있는지 확인하고 싶을 때 사용한다.

## Point.move
```java
package ch06.sec01;

public class Point {
    private int x, y;
    public Point(int x, int y) { this.x = x; this.y = y; }
    public int getX() { return x; }
    public int getY() { return y; }
    protected void move(int x, int y) {this.x = x; this.y = y; }
}
```

## Point3D.move
```java
package ch06.sec01;

public class Point3D extends Point{
    int z;
    public Point3D(int x, int y, int z) {
        super(x, y);
        this.z = z;
    }
    public void moveUp(){
        this.z += 1;
    }

    public void moveDown(){
        this.z -= 1;
    }
    public void move(int x, int y, int z){
        super.move(x, y);
        this.z = z;
    }
//    @Override
//    public void move(int x, int y){
//        super.move(x,y);
//    }

    @Override
    public String toString(){
        return "The point at ("+ super.getX() +", "+ super.getY() +", "+ this.z +")";
    }


}
```

여기서 super.move(x, y)를 사용할 필요는 없다.