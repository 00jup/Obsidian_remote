
```kotlin
TextButton(  
    onClick = { goToRegisterPage() },  
    // {} 안에 goToRegisterPage 하면 그냥 반환값  
    modifier = Modifier.align(Alignment.End)  
) {  
    Text(text = "Register your email")  
}
```

이렇게 했을 때 goToRegisterPage를 {}로 감쌀 거면 함수라고 알려줘야 함

그렇게 하면 안됩니다. `val clickHandler = onBackClicked()`는 변수를 선언하는 즉시 함수가 실행되어 버립니다.

예를 들어보겠습니다:

```kotlin
// 잘못된 방법
val clickHandler = onBackClicked()  // 변수 선언 시점에 즉시 함수가 실행됨
Button(onClick = clickHandler)  // ⚠️ 컴파일 에러: Unit 타입을 () -> Unit 타입에 할당할 수 없음

// 올바른 방법
val clickHandler = { onBackClicked() }  // 람다로 감싸서 나중에 실행되게 함
Button(onClick = clickHandler)  // ✅ 버튼 클릭 시 함수가 실행됨

// 또는 직접 Button에서 정의
Button(onClick = { onBackClicked() })  // ✅ 가장 일반적인 방법
```

Button의 onClick은 `() -> Unit` 타입의 함수를 파라미터로 받기 때문에, 함수의 실행 결과(Unit)가 아닌 실행할 함수 자체를 전달해야 합니다.


```kotlin
                modifier = Modifier.fillMaxWidth(), value = email, onValueChange = { email = it },
```

이렇게 값을 입력 가능하다

> email = it 는 아래와 같이 변환 가능하다.
> value -> email = value 임


```kotlin
(if(currentUser != null) currentUser.email else "No user")?.let {  
    Text(  
        text = it,  
        style = typography.titleLarge  
    )
```

전체 결과가 null이 아닌 경우에만 let을 수행해라