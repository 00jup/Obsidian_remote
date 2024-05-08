`async` 키워드를 함수에 추가하면 해당 함수는 비동기 함수가 되며, 아래와 같은 특징과 변화를 가져옵니다:

1. **Future 반환**: `async`로 표시된 함수는 항상 `Future`를 반환합니다. 만약 함수의 반환 타입이 명시적으로 정의되지 않았다면, 그 함수는 `Future<void>`를 반환하게 됩니다. 예를 들어, 값을 반환하는 비동기 함수의 경우 `Future<T>`의 형태로 반환타입을 가지게 됩니다, 여기서 `T`는 실제 반환하려는 값의 타입입니다.

2. **await 사용 가능**: `async` 함수 내부에서는 `await` 키워드를 사용할 수 있게 됩니다. `await`는 `Future`를 반환하는 다른 비동기 함수를 호출할 때 사용되며, 해당 `Future`가 완료될 때까지 함수의 실행을 일시 중단합니다. 이를 통해 비동기 코드를 마치 동기 코드처럼 쓸 수 있게 됩니다.

3. **비동기 실행**: `async` 함수는 호출되었을 때 즉시 `Future` 객체를 반환하고, 함수의 본문은 비동기적으로 실행됩니다. 즉, 함수 호출이 블로킹되지 않고 즉시 다음 코드로 진행됩니다.

4. **오류 처리**: `async` 함수 내에서 발생하는 오류는 `Future` 내에서 캡처되며, 이 `Future`에 `.catchError`나 `.then`과 같은 메서드를 사용하여 오류를 처리할 수 있습니다. 또한 `try-catch` 블록을 사용하여 `await` 호출에서 발생하는 오류를 처리할 수 있습니다.

예제:
```dart
Future<void> fetchData() async {
  try {
    var data = await someAsyncFunction();
    print(data);
  } catch (error) {
    print('Error occurred: $error');
  }
}
```

`async`와 `await`는 Dart와 같은 프로그래밍 언어에서 비동기 프로그래밍을 간소화하고 가독성을 향상시키기 위해 도입된 기능입니다.

[[Flutter 부모 자식 모두 async를 사용할 수 있다?]]
