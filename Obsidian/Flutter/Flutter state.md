부모가 보내고
자식에서 등록하고
자식에서 가져다 쓴다

```dart
getData() async { 
	var result = await 
	http.get(Uri.parse('https://codingapple1.github.io/app/data.json'));
	var result2 = jsonDecode(result.body); 
	setState((){ 
	data = result2; })
	 }
```
여기서 `setState()` 를 통해서 state를 설정한다.
## 부모가 보내고

그 다음 부모 위젯의 아래로 내려가서 `Scaffold` 안에 있는 FirstView에서 State를 보낸다.
```dart
FirstView(state : state)
```

## 자식에서 등록하고
```dart
class FirstView extends StatefulWidget {
	 const FirstView({super.key, this.state});
	 final state;
	 @override
  State<FirstView> createState() => _FirstViewState();
}
```

## 자식에서 가져다 쓴다
```dart
Column(
              children: [
                Image.network(widget.state[i]['image']),
                Padding(
                  padding: const EdgeInsets.all(8.0),
                  child: Align(
                    alignment: Alignment.centerLeft,
                    child: Column(
                      crossAxisAlignment: CrossAxisAlignment.start,
                      children: [
                        IconButton(
                          icon: Icon(Icons.thumb_up),
                          onPressed: () {},
                        ),
                        Text(widget.state[i]['likes'].toString() ?? '0'),
                        Text(widget.state[i]['content'] ??
                            'Default Content'),
                      ],
                    ),
```

[[Flutter ? 정리]]


## 부모위젯 PageView도 포함하고 있음
```dart
class _MyAppState extends State<MyApp> {
  var tab = 0;
  var data;
  final PageController _controller = PageController(); // [1]

  Future getData() async {
    var result = await http
        .get(Uri.parse('https://codingapple1.github.io/app/data.json'));
    if (result.statusCode == 200) {
      print('success');
    } else {
      throw Exception('Failed to load data');
    }
    data = json.decode(result.body);
    print(data);
  }

  @override //MyApp 위젯이 로드될 때 실행되는 함수
  void initState() {
    super.initState();
    getData();
  }

  @override
Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(
          "instagram",
          style: a,
        ),
        actions: [
          IconButton(onPressed: () {}, icon: Icon(Icons.add_box_outlined))
        ],
      ),
      body: PageView(
        controller: _controller, // [2]
        onPageChanged: (i) {
          setState(() {
            tab = i;
          });
        },
        children: [
          FirstView(sendedData: data),
          Container(
            color: Colors.blue,
          ),
        ],
      ),
      bottomNavigationBar: BottomNavigationBar(
        currentIndex: tab, // [3]
        showSelectedLabels: false,
        showUnselectedLabels: false,
        onTap: (i) {
          setState(() {
            tab = i;
            _controller.animateToPage(i, // [4]
                duration: Duration(milliseconds: 10),
                curve: Curves.easeInOut);
          });
        },
        items: [
          BottomNavigationBarItem(icon: Icon(Icons.home), label: "home"),
          BottomNavigationBarItem(
              icon: Icon(Icons.shopping_bag_outlined), label: "shopping"),
        ],
      ),
    );
  }
}

```

## 자식 위젯

```dart
class FirstView extends StatefulWidget {
  const FirstView({super.key, this.sendedData});
  final sendedData;

  @override
  State<FirstView> createState() => _FirstViewState();
}

class _FirstViewState extends State<FirstView> {
  ScrollController _scrollController = ScrollController();
  @override
  Widget build(BuildContext context) {
    if (widget.sendedData != null) {
      return ListView.builder(
          physics: ClampingScrollPhysics(),
          controller: _scrollController,
          itemCount: widget.sendedData?.length ?? 0,
          itemBuilder: (context, i) {
            return Column(
              children: [
                Image.network(widget.sendedData[i]['image']),
                Padding(
                  padding: const EdgeInsets.all(8.0),
                  child: Align(
                    alignment: Alignment.centerLeft,
                    child: Column(
                      crossAxisAlignment: CrossAxisAlignment.start,
                      children: [
                        IconButton(
                          icon: Icon(Icons.thumb_up),
                          onPressed: () {},
                        ),
                        Text(widget.sendedData[i]['likes'].toString() ?? '0'),
                        Text(widget.sendedData[i]['content'] ??
                            'Default Content'),
                      ],
                    ),
                  ),
                ),
              ],
            );
          });
    } else {
      return Center(
        child: CircularProgressIndicator(),
      );
    }
  }
}

```