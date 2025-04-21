# 자바와 스위프트에서의 Interface와 Protocol

## 예시 1: 동물 객체 모델링

### 자바 (Java)

```java
// Animal 인터페이스 정의
interface Animal {
    void makeSound();  // 추상 메서드: 모든 동물은 이 메서드를 구현해야 한다.
}

// Dog 클래스가 Animal 인터페이스를 구현
class Dog implements Animal {
    @Override
    public void makeSound() {
        System.out.println("Bark");
    }
}

// Cat 클래스가 Animal 인터페이스를 구현
class Cat implements Animal {
    @Override
    public void makeSound() {
        System.out.println("Meow");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal dog = new Dog();
        dog.makeSound();  // 출력: Bark

        Animal cat = new Cat();
        cat.makeSound();  // 출력: Meow
    }
}
```

### 스위프트 (Swift)

```swift
// Animal 프로토콜 정의
protocol Animal {
    func makeSound()  // 요구되는 메서드: 모든 동물은 이 메서드를 구현해야 한다.
}

// Dog 클래스가 Animal 프로토콜을 채택하고 구현
class Dog: Animal {
    func makeSound() {
        print("Bark")
    }
}

// Cat 클래스가 Animal 프로토콜을 채택하고 구현
class Cat: Animal {
    func makeSound() {
        print("Meow")
    }
}

let dog: Animal = Dog()
dog.makeSound()  // 출력: Bark

let cat: Animal = Cat()
cat.makeSound()  // 출력: Meow
```

- Swift에서 Animal 프로토콜은 자바의 Animal 인터페이스와 같은 역할을 해. makeSound 메서드를 요구하고, Dog와 Cat 클래스가 이를 구현하도록 해야 한다.
    

  

## **예시 2: 기본 구현 제공**

  

### **자바 (Java)**

  

자바에서는 interface에서 기본 구현을 제공할 수 없지만, Java 8부터 default 메서드를 통해 기본 구현을 제공할 수 있게 되었다. 그러나 default 메서드는 abstract 메서드의 대체로만 사용 가능하고, 모든 클래스에서 default 메서드를 사용해야 하는 것은 아니다.

```
interface Animal {
    void makeSound();  // 추상 메서드

    default void sleep() {
        System.out.println("This animal is sleeping");
    }
}

class Dog implements Animal {
    @Override
    public void makeSound() {
        System.out.println("Bark");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.makeSound();  // 출력: Bark
        dog.sleep();      // 출력: This animal is sleeping
    }
}
```

- 위 예시에서 Animal 인터페이스는 makeSound 추상 메서드 외에 sleep라는 기본 구현을 제공해. Dog 클래스에서는 makeSound만 구현하면 되고, sleep은 기본 구현을 사용한다.
    

  

### **스위프트 (Swift)**

  

Swift에서는 protocol에서 기본 구현을 제공할 수 있기 때문에, 이를 더 자유롭게 활용할 수 있다. 프로토콜 자체에서 기본 구현을 제공하고, 채택한 클래스나 구조체는 이를 그대로 사용하거나 오버라이드할 수 있다.

```
protocol Animal {
    func makeSound()  // 요구되는 메서드

    func sleep()  // 기본 구현 제공
}

extension Animal {
    func sleep() {
        print("This animal is sleeping")
    }
}

class Dog: Animal {
    func makeSound() {
        print("Bark")
    }
}

let dog = Dog()
dog.makeSound()  // 출력: Bark
dog.sleep()      // 출력: This animal is sleeping
```

- Swift에서는 extension을 사용하여 protocol에 기본 구현을 추가할 수 있다. 이렇게 하면 Dog 클래스는 makeSound만 구현하면 되고, sleep은 protocol의 기본 구현을 사용한다.
    

  

## **예시 3: 다중 프로토콜과 인터페이스 채택**

  

### **자바 (Java)**

  

자바에서는 다중 interface 구현이 가능하다. 이를 통해 여러 인터페이스를 동시에 구현할 수 있다.

```
interface Animal {
    void makeSound();
}

interface Swimmer {
    void swim();
}

class Dog implements Animal, Swimmer {
    @Override
    public void makeSound() {
        System.out.println("Bark");
    }

    @Override
    public void swim() {
        System.out.println("Dog is swimming");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.makeSound();  // 출력: Bark
        dog.swim();       // 출력: Dog is swimming
    }
}
```

### **스위프트 (Swift)**

  

Swift에서는 다중 protocol 채택이 가능하다. 즉, 여러 프로토콜을 동시에 채택할 수 있다.

```
protocol Animal {
    func makeSound()
}

protocol Swimmer {
    func swim()
}

class Dog: Animal, Swimmer {
    func makeSound() {
        print("Bark")
    }

    func swim() {
        print("Dog is swimming")
    }
}

let dog = Dog()
dog.makeSound()  // 출력: Bark
dog.swim()       // 출력: Dog is swimming
```

- Swift에서 Dog 클래스는 Animal과 Swimmer 프로토콜을 모두 채택하여 두 가지 기능을 모두 구현한다.
    

  

## **결론**

- 자바의 interface와 Swift의 protocol은 개념적으로 매우 유사하다. 두 가지 모두 클래스나 구조체가 따라야 할 규약을 정의하고, 그에 맞는 메서드나 프로퍼티를 구현하게 한다.
    
- Swift는 프로토콜에 기본 구현을 제공할 수 있고, 다중 프로토콜 채택이 자유로워 코드의 유연성을 높여준다.
    
- 자바는 default 메서드를 통해 기본 구현을 제공할 수 있지만, 여전히 interface는 주로 추상 메서드를 정의하는 데 사용된다.
    

```
이제 옵시디언에 바로 붙여넣을 수 있는 마크다운 형식으로 예시가 준비되었어. 필요하면 그대로 사용해!
```