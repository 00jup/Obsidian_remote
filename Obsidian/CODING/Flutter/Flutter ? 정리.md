[[Flutter 기본 정리]]
[[Flutter state]]

## Flutter에서는 nullable이 중요함
그래서 코드를 작성할 때, 아래와 같이 작성함
```dart
          itemCount: widget.sendedData?.length ?? 0,
                Image.network(widget.sendedData[i]['image']),
Text(widget.sendedData[i]['likes'].toString() ?? '0'),
                        Text(widget.sendedData[i]['content'] ??
                            'Default Content'),
```

?만 넣으면 null이 올 수도 있다는 뜻이고 (nullable) ??는 만약 null 이라면 우측의 값을 넣어라는 뜻

sendedData에는 다음과 같은 데이터가 담겨있음

```
[{id: 0, image: https://codingapple1.github.io/app/img0.jpg, likes: 5, date: July 25, content: 등을 대라 등대, liked: false, user: John Kim}, {id: 1, image: https://codingapple1.github.io/app/img1.jpg, likes: 22, date: Aug 3, content: 요즘 폰카는 성능이 좋습니다, liked: false, user: Hilton_m}, {id: 2, image: https://codingapple1.github.io/app/img2.jpg, likes: 10, date: Nov 30, content: 기린바보 😵, liked: false, user: rimvely1}]
```
`{id: 1, image: https://codingapple1.github.io/app/img1.jpg, likes: 22, date: Aug 3, content: 요즘 폰카는 성능이 좋습니다, liked: false, user: Hilton_m}`
그래서 이걸 자료형으로 표현하면,
Map<String, dynamic>임.

근데 왜 이렇게 될까?
```md
좋은 질문입니다! 주어진 데이터의 구조를 살펴보면, 각 키(key)는 문자열 타입이고, 값(value)은 여러 가지 타입이므로 `Map<String, dynamic>` 으로 타입을 지정합니다.

- `Map`: Dart에서 키-값 쌍으로 데이터를 저장하는 데이터 구조입니다.
- `<String, dynamic>`: 키는 `String` 타입이며, 값은 여러 가지 타입을 가질 수 있기 때문에 `dynamic`으로 지정합니다.

`dynamic`은 Dart에서 타입이 지정되지 않은, 즉 어떠한 타입이든 될 수 있는 유연한 타입을 의미합니다. 여기서 데이터는 다양한 타입의 값을 포함하고 있습니다.

- `id`: `int`
- `image`: `String`
- `likes`: `int`
- `da