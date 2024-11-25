
```kotlin
@Composable  
fun ChatScreen(navController: NavController, channelID: String, channelName: String) {  
    Scaffold(  
        containerColor = Color.Black  
    ) {  
        Column(  
            modifier = Modifier  
                .fillMaxSize()  
                .padding(it)  
        ) {  
            val viewModel: ChatViewModel = hiltViewModel()  
            LaunchedEffect(key1 = true) {  
                viewModel.listenForMessages(channelID)  
            }  
            val messages = viewModel.messages.collectAsState()  
            ChatMessages(channelName = channelName, messages = messages.value)  
            // 상태니까 messages.value임  
        }  
    }}
```