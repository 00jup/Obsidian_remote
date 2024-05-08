# Provider import

현재 lib 폴더 안에
main.dart 랑 profile.dart라는 폴더가 있다.

물론 pubspec.yaml 에서 dependencies 에서 provider:^6.0.5 는 추가한 상태이다.

main.dart에서 provider.dart를 import하고,

Store1이라는 클래스를 만들었다.

코드는 다음과 같다.

```dart

import 'package:provider/provider.dart';

class Store1 extends ChangeNotifier {
  var name = 'john kim';
}

```

provider에서 ChangeNotifierProvider를 MaterialApp에 감싸면

Profile() Widget이 당연히 MaterialApp에 있기 때문에 될 줄 알았다.

하지만 Profile() Widget에서 Store1에 있는 name을 사용하려면 다음과 같이 작성해야 한다.

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';
import 'main.dart';

class Profile extends StatelessWidget {
  const Profile({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(context.watch<Store1>().name),
      ),
      body: Center(
        child: Text(context.watch<Store1>().name),
      ),
    );
  }
}
```

main.dart 를 import 해야 한다.

다음으로는 `context.watch<Store1>().name`을 사용한다면 사용할 수 있다.

# 변수를 수정하는 법

State에서 변수를 수정할 때처럼 함수를 사용한다.

```dart
class Store1 extends ChangeNotifier {
  var name = 'john kim';

  /// 클래스 안 변수는 밖에서 수정한다면 위험하다고 여겨짐. 그래서 이렇게 코딩함.
  changeName() {
    name = 'john park';
    notifyListeners();
  }
}
```
setState는 사용할 수 없으므로, notifyListners를 사용한다.

# Tip

Watch -> 변수 읽고 싶을 때
Read -> 함수 실행하고 싶을 때



```dart
child: Text("팔로워 " + context.watch<Store1>().followers.toString()),
```

아래가 더 괜찮음

```dart
child: Text("팔로워 ${context.watch<Store1>().followers.toString()}명"),
```

[[Flutter Providers]]
[[Flutter CircleAvatar 설정]]
