Kotlin에서 람다 표현식이 함수의 마지막 파라미터일 때는 괄호 밖에 중괄호로 작성할 수 있는 특별한 문법을 제공한다.

```kotlin
// 두 가지 방법 모두 가능:

// 1. 모든 파라미터를 괄호 안에
ChannelItem(
    channelName = channel.name,
    onClick = { navController.navigate("chat/${channel.id}&${channel.name}") }
)

// 2. 마지막 람다 파라미터를 괄호 밖에
ChannelItem(channel.name) { 
    navController.navigate("chat/${channel.id}&${channel.name}") 
}
```

이런 문법을 "trailing lambda" 또는 "후행 람다"라고 부른다. 코드를 더 읽기 쉽게 만들어주며, 특히 Compose에서 자주 사용된다.
