
WarmMessageView의 Preview에서 @Binding으로 userName을 쓰고 있는데

TownView에서 

```swift
.sheet(isPresented: $showWarmMessage) { WarmMessagePopupView(isPresented: $showWarmMessage, userName : $responseManager.currentTownId) }
```


## WarmMessageView에서 #Preview
```swift
#Preview {
    let isPresented = Binding.constant(true)
    let userName = Binding.constant("테스트타운")
    
    return WarmMessagePopupView(isPresented: isPresented, userName: userName)
}
```