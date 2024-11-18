아름답구나

```kotlin
package com.example.coroutinetest  
  
import kotlinx.coroutines.async  
import kotlinx.coroutines.delay  
import kotlinx.coroutines.launch  
import kotlinx.coroutines.runBlocking  
import kotlinx.coroutines.yield  
  
enum class Product(val description: String, val deliveryTime: Long) {  
    DOOR("doors", 750),  
    WINDOWS("windows", 1250)  
}  
  
suspend fun order(item: Product): Product {  
    println("order: The ${item.description} are on the way")  
    //Thread.sleep(item.deliveryTime)  
    delay(item.deliveryTime)  
    println("order: The ${item.description} have arrived")  
    return item  
}  
  
suspend fun perform(taskName: String) {  
    println("task: Start $taskName")  
//    Thread.sleep(1000)   
delay(1000) // 이러면 더 빨라짐  
    println("task: Finish $taskName")  
}  
  
fun main() {  
    runBlocking {  
        val windows = async { order(Product.WINDOWS) }  
        val doors = async { order(Product.DOOR)  }  
        launch {  
            perform("laying bricks")  
            //perform("installing ${windows.description}")  
            perform("installing ${windows.await().description}")  
            // 이렇게 하면 실제 값에 접근이 가능해진다.  
            perform("installing ${doors.await().description}")  
        }  
  
    }  
}  
  
  
//fun main() {  
//    runBlocking {  
//        launch {  
//            // file reading  
//            println("Job start")  
//            switchReadToDownload()  
//            //양보함  
//            println("File 1 reading")  
//            switchReadToDownload()  
//            println("File 2 reading")  
//        }  
//        launch {  
//            // file download  
//            println("File 1 download")  
//            switchDownloadToRead()  
//            println("File 2 download")  
//            switchDownloadToRead()  
//            //thread는 cpu 운영체제에서 관리함. 성능저하가 일어나지만  
//            //coroutine은 cpu의 자원을 차지하는 것이 아닌 라이브러리로 한 쓰레드 안에서 써서 다르다.  
//        }  
////        yield()  
//        println("dddd")  
//    }  
////    runBlocking {  
////        // 1. join 사용  
////        val job1 = launch {  
////            println("Job start")  
////            yield()  
////            println("File 1 reading")  
////        }  
////        val job2 = launch {  
////            println("File 1 download")  
////        }  
////        job1.join() // job1이 끝날 때까지 대기  
////        job2.join() // job2가 끝날 때까지 대기  
////        println("dddd")  
////  
////        // 2. yield 사용  
////        launch {  
////            println("Job start")  
////            println("File 1 reading")  
////        }  
////        launch {  
////            println("File 1 download")  
////        }  
////        yield() // 다른 코루틴에게 실행 기회를 줌  
////        println("dddd")  
////    }  
////    // yield() 여기서는 하면 오류남.  
//}  
//  
//suspend fun switchReadToDownload(){  
//    println("Switching from Reading to Download")  
//    yield()  
//}  
//  
//suspend fun switchDownloadToRead(){  
//    println("Switching from Reading to Download")  
//    yield()  
//}
```