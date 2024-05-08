> widget.sendedData != null
> widget.sendedData.isNotEmpty


Future.builder의 경우 잘 바뀌지 않는 페이지에서 사용함
일반적으로 ListView.builder를 사용함.

Flutter와 Dart에서는 null safety를 도입하여 코드의 안정성을 향상시켰습니다. null safety는 Dart 2.12 버전부터 도입되었습니다. 이를 통해 개발자는 값이 null일 수 있는 변수와 그렇지 않은 변수를 명확하게 구분할 수 있게 되었습니다.

다음은 Flutter와 Dart에서 null과 관련된 주요 표현법과 개념들입니다:

1. **Nullable 변수**: 변수 뒤에 `?`를 붙여 해당 변수가 null 값을 가질 수 있음을 나타냅니다.
   ```dart
   int? nullableInteger;
   ```

2. **Non-nullable 변수**: 기본적으로 모든 변수는 non-nullable로 간주됩니다. 이는 해당 변수가 null 값을 가질 수 없다는 것을 의미합니다.
   ```dart
   int nonNullableInteger = 5;
   ```

3. **Late 키워드**: 변수가 초기화되기 전까지 null 값을 가질 수 있지만, 초기화 후에는 null이 아닌 값을 가지게 될 것임을 보장하는 키워드입니다.
   ```dart
   late int lateInitializedInteger;
   ```

4. **`!` 연산자 (bang operator)**: nullable 변수가 실제로 null이 아님을 확신할 때 사용합니다. 이 연산자를 사용하면 nullable 변수를 non-nullable로 간주합니다.
   ```dart
   int? nullableInteger = 5;
   int value = nullableInteger!;
   ```

5. **`??` 연산자**: 왼쪽의 표현식이 null이면 오른쪽의 값을 반환합니다.
   ```dart
   int? value = null;
   int result = value ?? 10;  // result는 10이 됩니다.
   ```

6. **`?.` 연산자**: 객체가 null이면 해당 연산을 수행하지 않고 null을 반환합니다.
   ```dart
   String? name;
   int? length = name?.length;  // name이 null이므로 length도 null입니다.
   ```

7. **null check 조건문**: 값이 null인지 확인하는데 사용합니다.
   ```dart
   int? nullableValue;

   if (nullableValue == null) {
     print('Value is null');
   }
   ```

이러한 표현법과 연산자들은 Dart의 null safety 기능을 지원하기 위해 도입된 것입니다. 코드에서 null 관련 오류를 최소화하기 위해 이러한 기능들을 적절히 활용하는 것이 좋습니다.

## 예시
```dart
Text(
                            "좋아요 ${widget.sendedData[i]['likes'].toString() ?? '0'}"),
                        Text(widget.sendedData[i