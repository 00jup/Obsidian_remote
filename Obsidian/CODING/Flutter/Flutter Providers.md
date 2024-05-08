> **store가 많은 경우 store 등록하는 법**

실은 ChangeNotifierProvider()를 store 갯수만큼 2중첩 3중첩하면 됩니다.

근데 그걸 쉽게 바꿔주는 문법도 있는데 

MultiProvider()로 바꿔서 감싸면 됩니다.

```dart
MultiProvider(
    providers: [
      ChangeNotifierProvider(create: (c) => Store1()),
      ChangeNotifierProvider(create: (c) => Store2()),
    ],
    child: MaterialApp( 어쩌구 ),
), 
```

그 안에는 ChangeNotifierProvider() 를 여러개 사용가능합니다.

맘대로 원하는 만큼 등록하도록 합시다.

그럼 이제 똑같이 모든 자식 위젯들은 Store1, Store2에 있던 state를 이용가능합니다.

이렇게 쓰시고 store 갯수 많아지면 언제나 다른 파일로 빼는게 좋겠군요. 

> **Provider 쓰면 get요청은?**

예를 들어서 Profile() 페이지 방문시

서버에 get요청을 날려서 데이터 받아오고 그걸 state에 보관하고싶으면 어떻게하냐는 말입니다.

http.get() 쓰면 되는건 맞는데 쓰는 위치는 초이스가 2개 있습니다. 

1. Profile의 initState안에서 get요청 날리고 

get요청이 완료되면 state수정함수를 작동시키거나

2. Profile의 initState안에서 state수정함수를 작동시켜서

state수정함수 안에서 get요청을 날리거나

맘대로 하면 됩니다.

하지만 state 관련된 모든 로직들은

store 안에 보관하는게 나중에 디버깅도 쉽기 때문에 거기에 넣어보도록 하겠습니다.

```dart
class Store1 extends ChangeNotifier {
  var profileImage = [];

  getData() async {
    var result = await http.get(Uri.parse('https://codingapple1.github.io/app/profile.json'));
    var result2 = jsonDecode(result.body);
    profileImage = result2;
    notifyListeners();
  }
}
```

1. profileImage라는 state를 만들었습니다.

2. get요청해서 그 결과를 profileImage 라는 state에 넣어주는 getData() 함수를 만들었습니다.

```dart
ElevatedButton(
  onPressed: (){
    context.read<Store1>().getData();
  }, 
  child: Text('사진가져오기')
)
```

3. 버튼 눌렀을 때 getData()를 실행했더니 진짜 서버에서 데이터 가져와서 profileImage에 넣어줍니다.

진짠지 출력해보십시오

아무튼 서버에서 데이터 가져오고, 보내고 싶으면 이런 식으로 하면 되겠습니다. 

(참고) 

Q. get, set 키워드 써도 되나요?

store만드는 class 안에서 굳이 의미없는 getter setter 만들 필요 없습니다.

Lint도 뭐라고 할걸요 

https://dart-lang.github.io/linter/lints/unnecessary_getters_setters.html