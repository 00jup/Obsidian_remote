
> Remotecontrol rc = new Audio(); 와 같이 사용하는 이유

# 1 rc에 다른 변수를 넣을 수 있음

```java
interface Remotecontrol(){
	void turnOn();
}
```

```java
class Audio implements RemoteControl(){
	public void turnOn(){
		System.out.println("Turn on Audio");	
	}
}
```

```java
class Tv implements RemoteControl(){
	public void turnOn(){
		System.out.println("Turn on Tv");	
	}
}
```

```java
class RemoteControlExample(){
	public static void main(){
		Remotecontrol rc = new Audio();
		rc.turnOn();
		rc = new Tv();
	}
}
```

# 2 public Control(RemoteControl rc)