
아니 WarmMessageView의 Preview에서 @Binding으로 userName을 쓰고 있는데 TownView에서 .sheet(isPresented: $showWarmMessage) { WarmMessagePopupView(isPresented: $showWarmMessage, userName : $responseManager.currentTownId) }

