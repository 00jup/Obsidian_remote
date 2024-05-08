여기서 비동기, private와 같은 개념이 이렇게 사용된다는 점을 처음 알게 되었다.
[[Flutter Class]]

```dart
  ScrollController _scrollController = ScrollController();
```
이렇게 객체를 생성했을 때 `_`가 들어간다는 것은 
private하게 사용한다는 것이다.

Dart에서 `_` (underscore) 접두사를 사용하지 않으면 해당 변수, 메서드, 클래스는 "public"으로 간주됩니다. 이 말은, 그 항목이 속한 Dart 파일(라이브러리)을 임포트하는 다른 Dart 파일에서 해당 항목을 접근할 수 있다는 것을 의미합니다.

예를 들면:

`a.dart` 파일:
```dart
class A {
  String publicField = "public in A";
}

class _B {
  String anotherField = "private class in A";
}
```


`b.dart` 파일:
```dart
import 'a.dart';

void main() {
  var a = A();
  print(a.publicField);  // "public in A" 출력. publicField는 공개되어 있기 때문에 접근 가능합니다.

  // var b = _B();  // 에러! _B 클래스는 a.dart 파일 내에서만 접근 가능합니다.
}
```

> 객체를 사용할 때 A()로 사용한다.
> ScrollController의 경우에도 이와 같이 ScrollController _scrollController = ScrollController();로 사용한다.


위 예제에서 `publicField`는 어디서든 접근할 수 있는 반면 `_B` 클래스는 `a.dart` 내에서만 접근 가능합니다.

그러나, 이 "public" 개념은 패키지 경계를 넘어서지 않습니다. 즉, Dart 패키지의 외부에 공개하려면 `pubspec.yaml`에 `export` 구문을 사용해야 합니다.



그래서 여기 안에서만 이걸 사용하겠다는 뜻으로 볼 수 있다.

```dart
@override
  void initState() {
    super.initState();
    _scrollController.addListener(() async {
      if (_scrollController.position.pixels ==
          _scrollController.position.maxScrollExtent) {
        getData();
      }
    }); //사용 다 끝나면 제거하는 것도 있음 찾아보기 ******************
    //스크롤 방향도 검사 가능하다 -> userScrollDirection
    //maxScrollExtent -> 스크롤바 최대 내릴 수 있는 높이
  }
```

여기서 async를 사용한다는 것은 비동기적으로 함수가 작동할 수 있다는 것이다.

근데 원래 getData()를 이 함수 안에 만들어서 async를 구현했지만 그냥 사용했다.
[[Flutter async]]

```dart
Future getData