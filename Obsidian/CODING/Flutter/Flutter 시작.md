> **프로젝트 시작은 main.dart 켜서** 

```dart
import 'package:flutter/material.dart';
 
void main() {
  runApp(
    MaterialApp(
      home : MyApp()
    )
  );
}

class MyApp extends StatelessWidget { 
  MyApp({Key? key}) : super(key: key); 
  @override 
  Widget build(BuildContext context) {

    return Scaffold();

  }
}
```

이렇게 채우고 시작할겁니다.

왜냐면 MaterialApp() 이건 밖으로 빼야 덜 불편하니까요. 

그리고 analysis_options.yaml 파일 열어서 

```dart
rules:
  prefer_typing_uninitialized_variables: false
  prefer_const_constructors_in_immutables: false
  prefer_const_constructors: false
  avoid_print: false
  prefer_const_literals_to_create_immutables: false 
```

이거 rules 부분에 추가하고 시작할겁니다. 

const 쓰라고하는건 필요없는 재렌더링을 막아서 쬐끔 성능향상때문에 쓰는건데 

나중에 앱 발행하기 전에 true로 바꿔서 써보든가 해보십시오. 

> **ThemeData() 에서 스타일 관리하기**

스타일을 넣을 때 위젯마다 하나하나 스타일 넣으면

코드가 금방 더러워집니다.

그래서 모든 위젯을 한 번에 스타일 넣을 수 있는 공간이 있는데

MaterialApp() 안에 ThemeData()를 열면 됩니다. 

```dart
MaterialApp(
  theme : ThemeData(),
  home : MyApp()
)
```

theme : ThemeData() 를 넣어보십시오.

이제 거기 안에 스타일 넣으면 모든 위젯들 스타일을 한 번에 결정할 수 있습니다.

> **ThemeData() 에 넣을 수 있는 것들** 

당연히 파라미터 안에 뭐 넣어야 뭐가 되는지 모를 땐

컨트롤 + space 누르면 자동완성되는 것들을 확인하면 됩니다. 

버튼, 글자, AppBar, 아이콘 등 많은 것들이 가능 

```dart
ThemeData(
  iconTheme: IconThemeData(color: Colors.red, size: 60),
  appBarTheme: AppBarTheme(
    color: Colors.grey,
  ),
)
```

예를 들면

iconTheme : IconThemeData() 여기 안에다가 빨간 스타일 넣으면 이제 모든 아이콘들이 빨개지고 

appBarTheme : AppBarTheme() 여기 안에다가 회색 배경색을 넣으면 모든 AppBar가 회색이 됩니다.

진짜 변했는지 아이콘과 앱바 넣어서 확인해보십시오. 

결론은 통일성 있는 UI 디자인 같은거 원하면 ThemeData 자주 활용해보십시오. 

레이아웃 짜던 코드도 깔끔해지고 좋음 

**Q. 스타일 중복이 발생하면?**

A. 나랑 물리적으로 가까운 스타일을 먼저 적용하려고 합니다.

**Q. 분명 ThemeData() 에 모든 아이콘을 파란색으로 칠해놨는데**

AppBar 안의 actions: [] 아이콘엔 적용이 안되는 것?

A. 복잡한 위젯은 복잡한위젯Theme() 안에서 스타일 줘야 잘 작동합니다.

그래서 AppBarTheme() 안에서 아이콘 스타일 주면 됩니다. 

그런 위젯들이 있다고 외울 순 없어서 언제나 검색으로 해결해야합니다. 

Dialog() 스타일 넣으려면 dialogTheme: DialogTheme(),

SnackBar() 스타일 넣으려면 snackBarTheme : SnackBarThemeData(),

TimePicker() 스타일 넣으려면 timePickerTheme: TimePickerThemeData(),

매우 많습니다. 

> **Text()의 스타일을 변경하고 싶으면**

```dart
ThemeData(
  textTheme: TextTheme(
    bodyText2: TextStyle(
        color : Colors.blue,
    ),
  ),
)
```

textTheme 쓰면 됩니다. 

근데 이상하게도 안에서 bodyText2 라는 것의 스타일을 변경해야합니다.

textTheme 안에서 정할 수 있는 것들 중에

headline1

headline2

bodyText1

bodyText2

subtitle1

이런 글자 스타일 종류들이 있는데

Text 위젯은 이 중에 bodyText2 스타일을 사용하고 

AppBar와 Dialog 위젯은 이 중에 headline6을 사용하고 

ListTile 위젯은 이 중에 subtitle1을 사용하고

그런 식으로 정해져있습니다. 

그래서 글자스타일은 그냥 변수에 저장해놓고

```dart
var text1 = TextStyle(color : Colors.red);
Text('글자', style : text1) 
```

이렇게 쓰는 식으로 코드짜는게 훨씬 편리합니다. 

변수에 넣어두면 재사용도 편리해지겠군요.

---
네, 맞습니다. 기본적으로 `flutter create` 명령을 사용하면 Android, iOS, 그리고 (Web 지원이 활성화된 경우) Web용 코드와 함께 macOS 용 코드도 생성됩니다.

특정 플랫폼만 포함하도록 Flutter 프로젝트를 생성하려면 `--platforms` 옵션을 사용할 수 있습니다. 예를 들어, Android, iOS, 그리고 Web만을 위한 프로젝트를 생성하려면 다음과 같이 명령어를 사용할 수 있습니다:

```bash
flutter create --platforms android,ios,web <프로젝트 이름>
```

위의 명령어는 macOS용 코드를 생성하지 않습니다. 이러한 방법으로 원하는 플랫폼만을 대상으로하는 Flutter 프로젝트를 생성할 수 있습니다.