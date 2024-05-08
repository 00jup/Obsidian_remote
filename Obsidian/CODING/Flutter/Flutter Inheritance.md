[[Flutter provider]]


### 1. 기본 생성자 
가장 기본적인 형태입니다. 상위 클래스의 생성자에 파라미터를 전달합니다.

```dart
class BoyGroup extends Idol {
  BoyGroup(String name, int membersCount) : super(name : name, membersCount : membersCount);
}
```

### 2. Named Constructor
`BoyGroup`에 특정한 생성 방식을 제공하려면 named constructor를 사용할 수 있습니다.

```dart
class BoyGroup extends Idol {
  BoyGroup.newDebut(String name) : super(name, 0);
}
```

이 경우, `BoyGroup.newDebut("NewGroup")`으로 새로 데뷔하는 그룹을 0 멤버로 생성할 수 있습니다.

### 3. 기본값 포함 생성자
`membersCount`에 기본값을 제공하는 생성자를 만들 수 있습니다.

```dart
class BoyGroup extends Idol {
  BoyGroup(String name, [int membersCount = 5]) : super(name, membersCount);
}
```

이 경우, `BoyGroup("SomeGroup")`로 객체를 생성하면 멤버 수가 기본적으로 5로 설정됩니다.

### 4. Factory Constructor
Factory 생성자를 사용하여 조건에 따른 객체를 반환할 수 있습니다.

```dart
class BoyGroup extends Idol {
  factory BoyGroup.specialGroup(String name, int membersCount) {
    if (membersCount > 10) {
      return BoyGroup("Super " + name, membersCount);
    }
    return BoyGroup(name, membersCount);
  }
  
  BoyGroup(String name, int membersCount) : super(name, membersCount);
}
```

이 경우, `specialGroup` 생성자를 사용하면 멤버 수가 10명 초과인 그룹 이름 앞에 "Super"가 붙습니다.

이러한 다양한 생성자를 제공함으로써 클래스의 사용법을 다양화하고, 유연하게 객체를 생성할 수 있게 만들 수 있습니다.

[[부모의 상속 함수와 자식의 상속 함수]]

### 동적인 UI 만드는 법
1. state에 현재 UI의 상태 저장
2. state에 따라 UI 어떻게 보일지 작성
3. 유저도 state 조작할 수 있게