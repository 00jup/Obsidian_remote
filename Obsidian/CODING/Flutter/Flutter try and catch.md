
try catch를 이용해 error을 찾을 수 있다.

```dart
getData() async {
    try {
      var result = await firestore.collection('product').get();
      for (var doc in result.docs) {
        print(doc['name']);
      }
    } catch (e) {
      print(e);
      print("error!!!!!");
    }
```

catch의 e의 경우 어떤 error를 포함하는지 정보를 가지고 있다.