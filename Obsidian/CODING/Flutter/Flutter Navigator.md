Navigator를 사용하는 방법은 다음과 같다.
```dart
IconButton(
              onPressed: () {
                Navigator.push(
                    context,
                    MaterialPageRoute(
                        builder: (context) =>
                            Upload() //하나 밖에 없을 때 arrowFunction 사용하기
                        ));
              },
              icon: Icon(Icons.add_box_outlined))
```
사용할 Widget이 하나 밖에 없을 때는 위와 같이 arrow function을 사용한다.

Upload 코드는 다음과 같다.
```dart
class Upload extends StatelessWidget {
  const Upload({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(),
        body: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Text('이미지업로드화면'),
            IconButton(
                onPressed: () {
                  Navigator.pop(context);
                },
                icon: Icon(Icons.close)),
          ],
        ));
  }
}
```

여기서 Navigator.pop(context);를 사용하면 밖으로 나가기 기능이 가능하다.

```dart
onPressed: () {
                  Navigator.pop(context);
                }
```

## 라우터 기능

웹을 만드는 것처럼 여러 개의 페이지를 만들고 싶으면 라우터를 사용한다.

/home -> Home()
/detail -> Detail()
/shop -> Shop()

코드는 다음과 같이 사용한다.

```dart
MaterialApp(
    initialRoute: '/',
    routes: {
      '/': (context) => Text('첫페이지'),
      '/detail': (context) => Text('둘째페이지'),
    },
);
```

//home: MyApp()
//MaterialApp 필요없음

복잡하고 많은 페이지 한번에 관리가 가능하다.

이렇게 처음 만들고 페이지를 이동하게 만들고 싶으면

```dart
Navigator.pushNamed(context, '/detail');
```

를 사용한다.

그니까 가끔가다가 /detail/1 이렇게 입력하면 1번 게시물을 보여주고 

/detail/2 이렇게 입력하면 2번 게시물을 보여주는

그런 앱을 만들고 싶다면 onGenerateRoute 라는 파라미터를 써야하는데

```dart
MaterialApp(
      initialRoute: '/',
      onGenerateRoute: (settings) {
        var arguments = settings.arguments;
        if (settings.name == '/detail') {
          return MaterialPageRoute(builder: (context) => Upload(routeparam : arguments) );
        } else if (settings.name == '/') {
          return MaterialPageRoute(builder: (context) => Text('홈페이지') );
        } else {
          return null;
        }
      },
);
```

/detail/1 로 이동하면 routeparam이라는 파라미터가 1로 변하고

/detail/2 로 이동하면 routeparam이라는 파라미터가 2로 변합니다. 

그리고 routeparam의 값은 Upload() 위젯 안에서 등록하고 사용가능합니다. 

굳이 따라 쓸 필요는 없고 이런게 있다고만 알고 지나가면 되겠습니다.

실은 각각 다른 정보를 위젯 안으로 보내고 싶으면 굳이 라우터 + 파라미터 기능으로 구현할 필요 없습니다.

예전에 했던 state를 자식 위젯으로 보내는거 그거 써도 될듯요 

근데 왜 가르쳤냐고요?

코드양이 많으면 고급기술 많이 배운것 같은 느낌들어서 아조씨들이 좋아하기 때문입니다.

2. 라우터는 페이지가 많을 때 관리하기 편하려고 쓰는 것일 뿐입니다. 지금은 필요없겠군요 

3. 라우터를 본격적으로 써야한다면 패키지 설치해서 쓰는게 낫습니다.

VRouter 이런거 찾아 설치해서 쓰면 Vue, React 라우터처럼 직관적이고 깔끔한 문법으로 페이지 나누기 가능합니다.

구글이 만든 소프트웨어들은 기본 사용법이 언제나 거지같아서 외부 패키지 설치하는게 낫습니다.


