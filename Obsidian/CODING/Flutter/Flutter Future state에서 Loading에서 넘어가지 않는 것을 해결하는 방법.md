[[Flutter state]]
[[Flutter async]]


## setState를 사용한다.
```dart
if(result.statusCode == 200) {
      print('success');
    } else {
      throw Exception('Failed to load data');
    }
    data = json.decode(result.body);
    setState(() {
      sendedData = data;
    });
```

원래는 data를 그대로 FirstPage(sendedData : data) 이렇게 보냈음.

근데 setState로 설정 후 사용하니까 loading 창이 바뀌는 것이 적용됨.

```
  
Flutter에서 `setState`는 `StatefulWidget`의 상태를 변경할 때 사용됩니다. `setState`를 호출하면 Flutter는 위젯을 다시 빌드(rebuild)하여 UI에 변경된 상태를 반영합니다.

여기서 `data` 변수는 비동기적으로 데이터를 가져온 후에 업데이트됩니다. 데이터가 변경되면, 이를 UI에 반영하기 위해서는 해당 위젯을 다시 빌드해야 합니다. `setState`를 사용하면 이를 쉽게 할 수 있습니다.

만약 `setState`를 사용하지 않고 데이터를 변경한다면, 변경된 `data`의 값은 내부 상태에는 반영되겠지만 UI에는 바로 반영되지 않을 것입니다. 다른 요인으로 인해 위젯이 다시 빌드되기 전까지는 변경된 데이터가 화면에 나타나지 않습니다.

따라서, 상태가 변경될 때마다 UI를 즉시 업데이트하려면 `setState`를 사용해야 합니다.
```

그렇다고 한다..

+) setState 함수는 콜백 함수이다. 그래서 위젯 상태를 변경하는 코드를 넣을 수 있음. 또 보통 파라미터로 어떤 것도 넣지 않는다.



근데 아직 왜 isNotEmpty 함수가 안 되는지는 잘 모르겠음.