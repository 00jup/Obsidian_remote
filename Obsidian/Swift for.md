
```swift
**let** interestingNumbers = [

    "Prime": [2, 3, 5, 7, 11, 13],

    "Fibonacci": [1, 1, 2, 3, 5, 8],

    "Square": [1, 4, 9, 16, 25],

]

**var** largest = 0

**for** (_, numbers) **in** interestingNumbers {

    **for** number **in** numbers {

        **if** number > largest {

            largest = number

        }

    }

}
```

underlined 처리해도 인식 가능함.
