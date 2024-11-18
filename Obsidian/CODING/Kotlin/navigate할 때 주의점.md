
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

```kotlin
                modifier = Modifier.fillMaxWidth(), value = email, onValueChange = { email = it },
```

이렇게 값을 입력 가능하다

email = it -> value -> email = value 임


```kotlin
(if(currentUser != null) currentUser.email else "No user")?.let {  
    Text(  
        text = it,  
        style = typography.titleLarge  
    )
```

전체 결과가 null이 아닌 경우에만 let을 수행해라