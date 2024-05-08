스크롤 위치를 파악하고 싶으면 해당 위젯을 StatefulWidget으로 바꾸는게 좋습니다.

그러니까 우리 Home 위젯을 StatefulWidget으로 빨리 변경하십시오

전구버튼 누르면 쉬울듯

(참고) StatefulWidget은 class가 2개입니다.

부모가 보낸 state를 등록할 때는 윗 class에 등록하고

사용은 아랫 class에서 합니다.

아랫 class에서 윗 class에 있는 변수를 사용할 때는 **widget.변수명** 이렇게 씁니다.

`if (widget.sendedData != null)`

StatefulWidget으로 바뀌면 이렇게 적어야 함.