
## Flutter 클래스로 객체를 만드는 법

Flutter에서 클래스는 객체의 설계도와 같습니다. 객체는 속성(변수)과 동작(메서드)으로 구성됩니다.

예를 들어, `Idol`이라는 클래스를 정의하면 다음과 같이 작성할 수 있습니다:

```dart
class Idol {
  String name;
  List<String> members;

  Idol(this.name, this.members); // 기본 생성자
}
```

여기서 `Idol` 클래스는 두 개의 속성인 `name`과 `members`를 갖고 있습니다.

## constructor를 사용하는 방법 1

생성자를 사용하여 객체의 초기 상태를 설정할 수 있습니다. 생성자의 이름은 클래스의 이름과 동일합니다.

다음은 `name`과 `members` 속성을 초기화하는 생성자입니다:

```dart
class Idol {
  String name;
  List<String> members;

  // Constructor
  Idol(String name, List<String> members) {
    this.name = name;
    this.members = members;
  }
}
```

이를 통해 `Idol` 객체를 다음과 같이 생성할 수 있습니다:

```dart
Idol blackpink = Idol("blackpink", ['1', 'b', 'c', 'd']);
```

## constructor를 사용하는 방법 2

Dart에서는 생성자의 매개변수를 직접 클래스의 속성에 연결할 수 있습니다. 이를 통해 코드를 더 간결하게 만들 수 있습니다:

```dart
class Idol {
  String name;
  List<String> members;

  // Constructor
  Idol(this.name, this.members);
}
```

이 방법을 사용하면 이전 예제와 동일한 방식으로 객체를 생성할 수 있습니다.

## named constructor를 사용하는 방법

Dart는 여러 개의 생성자를 정의할 수 있도록 named constructor라는 기능을 제공합니다. 

예를 들면:

```dart
class Idol {
  String name;
  List<String> members;

  Idol(this.name, this.members); // 기본 생성자

  // Named Constructor
  Idol.fromList(List values) 
      : name = values[1], 
        members = values[0];
}
```

named constructor를 사용하여 객체를 생성하는 방법:

```dart
Idol bts = Idol.fromList(['1', 'rm', 'bb', 'sugar'], "BTS");
```

---
### Getter와 Setter 사용 이유와 예시

Getter와 Setter는 객체의 내부 상태를 안전하게 관리하기 위한 방법입니다.

- **Getter**: 객체의 특정 필드의 값을 가져오기 위해 사용합니다.


```dart
String get fristMember{
	return this.members[0];
	}
```


- **Setter**: 객체의 특정 필드의 값을 설정하기 위해 사용합니다.


```dart
set firstMember(String name){
	this.members[0] = name; 
}
```


Setter를 사용하면, 값을 설정할 때 추가적인 검증이나 변환 등의 작업을 삽입할 수 있어, 객체의 상태를 보다 안전하게 관리할 수 있습니다.

## 이름 앞에 _ 적는 이유

Dart에서 클래스나 변수, 함수 등의 이름 앞에 `_` (underscore)를 붙이는 것은 해당 항목이 **private**하다는 것을 나타냅니다. Dart의 접근 제어자는 다른 언어들과는 조금 다르게 동작합니다. Dart에서는 `public`, `private`, `protected` 같은 키워드를 제공하지 않습니다. 대신, 이름이 `_`로 시작하는 항목은 해당 라이브러리 내에서만 접근 가능하며, 라이브러리 외부에서는 접근할 수 없습니다.

예를 들어:

```dart
class Example {
  String publicData = 'I am public';  // 이 변수는 어디서든 접근 가능합니다.
  String _privateData = 'I am private';  // 이 변수는 Example 클래스나 같은 파일 내에서만 접근 가능합니다.
}
```

`controller: _scrollController,`에서 `_scrollController`는 private 변수로서, 해당 클래스나 동일한 파일 내의 다른 클래스에서만 접근 가능하다는 것을 나타냅니다. 이를 통해 코드의 의도를 명확하게 표현하고, 코드의 캡슐화를 유지하여 외부에서 의도치 않게 상태나 동작을 변경하는 것을 방지할 수 있습니다.

### _ 사용하는 이유

Dart에서 `_` (underscore)로 시작하는 멤버는 private 멤버로 간주되어 동일한 파일 내에서만 접근이 가능합니다. 그러나, 왜 이렇게 private 멤버를 사용해야 하는지에 대한 이유를 좀 더 자세히 설명하겠습니다:

1. **캡슐화 (Encapsulation)**: 
   - OOP (객체 지향 프로그래밍)의 핵심 원칙 중 하나는 캡슐화입니다. 캡슐화란 객체의 상태와 행동을 하나의 단위로 묶고, 외부로부터의 접근을 제한하는 것을 의미합니다.
   - Private 멤버를 사용하면 객체의 내부 상태와 동작을 숨길 수 있으며, 이를 통해 객체의 정확한 동작을 보장할 수 있습니다. 
   - 예를 들어, 클래스의 내부 로직에 따라 특정 변수의 값이 변경될 때마다 다른 동작이 수행되어야 하는 경우, 해당 변수를 private으로 설정하면 외부에서의 무분별한 접근을 방지하고 객체가 올바르게 동작하도록 할 수 있습니다.

2. **유지 보수성 (Maintainability)**:
   - 클래스의 내부 구현이 변경되더라도, 그 내부의 private 멤버만 변경되는 경우 외부 코드에는 영향이 없습니다. 이렇게 되면 코드의 유지 보수가 더 쉬워집니다.
   - 또한, 외부에서 접근할 수 없는 private 멤버는 해당 클래스나 파일 내에서만 변경을 고려하면 되므로 리팩토링이나 개선 작업이 더 간편해집니다.

3. **명확한 의도 표현 (Expressing Intent Clearly)**:
   - `_` (underscore)로 시작하는 멤버는 코드를 읽는 사람에게 "이 멤버는 내부적인 용도로만 사용됩니다"라는 명확한 메시지를 전달합니다.
   - 이를 통해 코드의 의도가 더 잘 전달되고, 다른 개발자들이 코드를 쉽게 이해하고 활용할 수 있습니다.

4. **오류 방지 (Preventing Mistakes)**:
   - 외부에서 접근이 제한된 private 멤버는, 그 멤버를 잘못 사용하거나 의도치 않게 변경하는 실수를 방지할 수 있습니다.

종합적으로, private 멤버 (Dart에서는 `_`로 시작하는 멤버)를 사용하는 것은 객체 지향 프로그래밍의 원칙을 지키고, 코드의 안정성, 유지 보수성을 향상시키며, 코드의 의도를 명확하게 전달하는 데 도움이 됩니다.


[[getter&setter와 객체지향의 관련성]]
[[const로 객체를 선언할 때의 장점]]
