
## 예시

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

int main()
{
    srand(time(NULL));
    int input, sum;
    int numb1, numb2;
    while (1)
    {
        numb1 = rand() % 10;
        numb2 = rand() % 10;
        printf("%d + %d = ", numb1, numb2);

        sum = numb1 + numb2;
        scanf("%d", &input);

        if (sum == input)
            printf("맞았습니다.\n");
        else if (input == -1)
            break;
        else
            printf("틀렸습니다.\n");
    }

    return 0;
}
```

### srand(time(NULL))을 해야 하는 이유

`rand()` 함수는 `srand()` 없이도 작동합니다. 그러나 `srand()`를 사용하지 않으면 `rand()` 함수는 기본적으로 동일한 시드 값을 사용합니다. 이는 프로그램을 다시 시작할 때마다 `rand()`가 동일한 난수 시퀀스를 생성하게 됨을 의미합니다.

이러한 특성은 몇 가지 상황에서 문제가 될 수 있습니다:

1. **테스트와 디버깅**: 동일한 난수 시퀀스가 반복적으로 생성되면, 특정 문제나 버그를 재현하기 위해 일관된 시나리오를 만들 수 있습니다. 따라서 테스트나 디버깅 과정에서는 동일한 시드를 사용하는 것이 유용할 수 있습니다.

2. **실제 응용 프로그램**: 대부분의 응용 프로그램에서는 매번 다른 난수 시퀀스를 원합니다. 예를 들어, 게임이나 시뮬레이션에서는 사용자가 매번 다른 경험을 얻기를 원합니다. 이 경우, `srand(time(NULL));`와 같이 시드 값을 변경하여 다양한 난수 시퀀스를 생성하는 것이 좋습니다.

결론적으로, `rand()`는 `srand()` 없이도 작동하지만, 동일한 시드 값에 의해 동일한 난수 시퀀스를 생성합니다. 이러한 동작이 원하는 결과와 일치하는지에 따라 `srand()`의 사용을 결정할 수 있습니다.