네, Dart 언어의 여러 기능에 대해 간단하게 정리하겠습니다.

---
[[Flutter Align]]
[[Flutter state]]
[[Flutter Future state에서 Loading에서 넘어가지 않는 것을 해결하는 방법]]
[[Flutter widget.변수명]]
[[Flutter null 표현]]
[[Flutter add vs addAll]]
[[widget.sendedData?.length ?? 0,]]
[[Flutter Navigator]]
[[Flutter image_picker]]
[[Flutter 삼항 연산자]]
[[Flutter @override]]
[[Flutter assets]]
[[Flutter 출력하는 법]]
[[Flutter 오류 생겼을 때]]



### &{data[i]};
### Dart Features

1. **Enum**
    - Enum은 정확한 값들만 가질 수 있음.
```dart
    enum Status{
      approved,
      pending,
      rejected,
    }
	void main() {
	  Status status = Status.approved;
	  //정확히 이 3개의 값만 존재한다고 이야기할 때, 사용한다.
	   status = Status.pending;
	}
    ```

2. **Nullable**
    - Dart에서는 변수가 null 값을 가질 수 있는지를 명시할 수 있음.
    - 변수 타입 뒤에 `?`를 붙여서 null 값을 가질 수 있음을 표현.
    - [[NULL]]
```dart
	String? name4 = "nn";
	name4 = null;
	name4 = null;
	print(name);
	print(name!); //null이 아니다!
	double? number = 10;
	//왜 var? number 하면 안 되는 거지?
	number ??= 3.8; //number가 null이면 오른쪽으로 바꿔라
```

3. **final & const**
    - `final`과 `const`는 둘 다 한 번 값을 할당하면 변경할 수 없음.
    - `const`는 컴파일 시점의 상수 값을 요구하기 때문에 `DateTime.now()`와 같이 런타임 값을 가지는 것을 사용할 수 없음.

4. **Map & Set**
    - Map은 key-value 쌍으로 데이터를 저장.
```dart
    Map<String, bool> dictionary = {
        'Harry' : true,
        "iron" : true,
    };
```

-   Set은 중복되지 않는 데이터를 저장.
```dart
    final Set<String> names5 = {
        'Harry',
        'Flutter',
    };
    ```

5. **While Loop**
    - 조건을 검사한 후에 루프 내부의 코드를 실행.
```dart
    while(total < 10){
        total += 1;
		print("${total} !");
		if(total == 5){
		  //continue;
		  break;
		}
		
		print("${total} !");
		}
    }
    ```

6. **Switch Case**
    - 변수의 값을 기준으로 여러 경우 중 하나를 실행.
```dart
    switch(num