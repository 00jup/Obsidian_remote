[[Flutter 기본 정리]]

Padding Widget 때문에 정렬이 되지 않는 경우가 존재합니다.
만약 `Padding` 위젯 때문에 왼쪽 정렬이 잘 되지 않는다면, `Align` 위젯을 사용하여 간단하게 내용을 왼쪽으로 정렬할 수 있습니다.

다음은 `Align` 위젯을 사용하여 수정한 코드 예시입니다:

```dart
class _FirstViewState extends State<FirstView> {
  ScrollController _scrollController = ScrollController();

  @override
  Widget build(BuildContext context) {
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
                  alignment: Alignment.centerLeft,  // 왼쪽 정렬
                  child: Column(
                    crossAxisAlignment: CrossAxisAlignment.start,
                    children: [
                      IconButton(
                        icon: Icon(Icons.thumb_up),
                        onPressed: () {},
                      ),
                      Text(widget.sendedData[i]['likes'].toString() ?? '0'),
                      Text(widget.sendedData[i]['content'] ?? 'Default Content'),
                    ],
                  ),
                ),
              )
            ],
          );
        });
  }
}
```

>Align(
                  alignment: Alignment.centerLeft, 

이 부분을 통해서 코드가 잘 작동하게 되었습니다.
`Align` 위젯을 사용하면 해당 위젯의 자식을 지정된 정렬 방식에 따라 정렬할 수 있습니다. `alignment: Alignment.centerLeft`를 설정하면 자식 위젯들이 왼쪽으로 정렬됩니다.

## Align을 사용하는 이유
좋은 질문입니다. `Align` 위젯의 사용 이유를 설명하겠습니다.

Flutter에서, 위젯들은 부모 위젯의 사용 가능한 공간에 따라 어떻게 배치될지 결정됩니다. 예를 들어, `Container`나 `Padding` 같은 위젯들은 일반적으로 가능한 전체 공간을 차지하려고 합니다. 그렇기 때문에 그 안에 있는 자식 위젯들은 부모 위젯의 전체 공간에 맞게 정렬되어야 합니다.

이때, `Align` 위젯은 부모 위젯의 사용 가능한 공간 내에서 자식 위젯을 특정 위치에 정렬하는 데 유용합니다. `Align` 위젯은 `alignment` 속성을 사용하여 정렬을 조절할 수 있습니다.

`Align` 위젯을 사용하는 주요 이유는:

1. **간단한 정렬**: `Align`은 자식 위젯을 쉽게 특정 위치에 정렬할 수 있습니다. 예를 들어, `Alignment.centerLeft`는 위젯을 중앙의 왼쪽에, `Alignment.bottomRight`는 오른쪽 하단에 정렬합니다.

2. **유연성**: `Align`은 부모의 사용 가능한 공간 내에서 자식 위젯의 위치를 조절할 수 있습니다. 따라서 여러 다양한 UI 요구 사항을 처리하는 데 유용합니다.

3. **코드 가독성**: `Align`을 사용하면, 코드를 읽는 사람에게 해당 위젯의 정렬 의도를 명확하게 표현할 수 있습니다.

위의 예제에서는 `Column` 위젯 내의 내용을 왼쪽으로 정렬하기 위해 `Align` 위젯을 사용했습니다. `Align` 없이도 `CrossAxisAlignment.start`를 사용하여 `Column`의 내용을 왼쪽으로 정렬할 수 있지만, `Padding` 위젯과 같은 다른 위젯들과의 상호 작용으로 인해 원하는대로 동작하지 않을 수 있습니다. 따라서 `Align`을 사용하여 명확하게 자식 위젯의 정렬을 지정하는 것이 좋습니다.