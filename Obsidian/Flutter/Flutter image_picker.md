Package 설치해야 함.

> **image_picker 설치와 셋팅**

폰의 사진파일 가져다쓸 땐 요즘은 허락받을 필요 없습니다. 그냥 쓸 수 있습니다.

1. pubspec.yaml 파일 열고 

```json
dependencies:
  image_picker: ^0.8.4+4
```

image_picker 추가하고 pub get 누르면 됩니다.

2. ios/Runner/Info.plist 파일 열고

```json
<key>NSPhotoLibraryUsageDescription</key>
<string>사진첩좀 써도 됩니까</string>
<key>NSCameraUsageDescription</key>
<string>카메라좀 써도 됩니까</string>
<key>NSMicrophoneUsageDescription</key>
<string>마이크 권한좀 제발</string>
```

이런 코드를 `<dict>` 하단에 추가하면 됩니다. 

사용자에게 허락팝업 띄울 때 보이는 글자들입니다. 

3. dart파일 맨 위에 

```dart
import 'package:image_picker/image_picker.dart';
import 'dart:io';
```

추가하면 됩니다. 

둘째는 파일 다루는 유용한 함수가 들어있는 기본 패키지입니다. 

> **image_picker 사용법**

AppBar 우측 버튼에 이렇게 코드를 짜봤습니다. 

```dart
onPressed: () async {
  var picker = ImagePicker();
  var image = await picker.pickImage(source: ImageSource.gallery);
}
```

저거 2줄 사용하면 이미지 선택화면이 뜹니다. 

저장된 사진이 없으면 폰으로 사진 몇장 찍어보십시오 

picker.pickImage(source: ImageSource.camera);

이러면 사진선택하는 갤러리 말고 카메라를 띄워줍니다.

picker.pickVideo(source: ImageSource.gallery);

이러면 비디오 선택화면이 뜹니다. 

picker.pickMultiImage(source: ImageSource.gallery);

이러면 여러 이미지 선택이 가능합니다. 

- 고른 이미지 사이즈, 화질 조정도 가능합니다. 

- photofilters 이런 패키지 설치하면 이미지에 필터도 씌울 수 있습니다.

> **선택한 이미지 다루기**

이미지는 용량이 크기 떄문에 

이미지를 변수에 저장해놓고 쓰는게 아니라 

이미지의 경로만 가져와서 변수에 저장하고 쓰는게 일반적입니다.

```dart
onPressed: () async {
  var picker = ImagePicker();
  var image = await picker.pickImage(source: ImageSource.gallery);
   if (image != null) {
    setState((){
      userImage = File(image.path);
    });
  }
  
}
```

그래서 상단에 var userImage 이런 state 하나 만들고

거기 저장하라고 했습니다. 선택 안하면 null 일까봐 if문으로 체크도 좀 해줬습니다.

근데 이걸 실제 위젯같은 곳에 보여주려면 어떻게 코드를 짜야하냐면 

> **선택한 이미지를 위젯으로 보여주려면**

Image.file(userImage) 이렇게 쓰면 보입니다.

이미지 파일경로를 넣으면 이미지로 보여주는 위젯입니다. 

Upload() 위젯안에 저걸 써서 보여주도록 합시다.

근데 userImage 이 변수는 MyApp() 위젯 안에 있네요?

![](https://codingapple.com/wp-content/uploads/2021/12/%EC%BA%A1%EC%B2%98.png)

그럼 MyApp -> Upload 이렇게 변수를 보내면 됩니다. 

보내고 Image.file(userImage) 이거 쓰면 이제 진짜로 보임

**오늘의 숙제 :** 

발행버튼 누르면 유저가 입력한글과 사진이 맨 위에 게시물로 뿅 나타나야합니다.

실제 서비스라면 글과 사진을 서버로 보내서 DB에 저장하겠지만

우린 서버가 없으니 그냥 위젯으로 보여주기만 하면 됩니다.

게시물 위젯으로 보여주려면 게시물 위젯을 만들어야하나~ 이런 생각할 필요가 없는게

아마 ListView.builder를 이용해서 var data안의 데이터로 게시물 반복생성하라고 해놨으니

var data 라는 state에 유저의 글과 사진 데이터만 더해주면 해결입니다.

## photofilters

package 있음

## 글을 쓰는 것도 있음

## 이미지가 깨질 때
1. resizeToAvoidBottomlnset
2. 이미지를 줄인다.
3. 글쓰는 페이지를 하나 더 만든다
4. 스크롤바를 만든다


발행버튼 누르면 글발행.
state에 수정하도록 하기
원래 게시물 map자료형을 하나로 만든다.
그리고 state에 추가하기


폰에서 고른 이미지는 Image.file()로 쓰기
