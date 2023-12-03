```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    srand(100);

    for (int i = 0; i < 10; i++)
    {
        printf("%d \n", rand());
    }
}
```

`rand()` 함수는 C 언어의 표준 라이브러리에 있는 난수 생성 함수이다. 이 함수는 호출할 때마다 0부터 `RAND_MAX`까지의 숫자 중 하나를 무작위로 반환한다.

그러나 `rand()` 함수 자체는 항상 동일한 난수 시퀀스를 생성한다. 매번 다른 난수 시퀀스를 얻기 위해서는 `srand()` 함수를 사용하여 난수 생성기의 초기값(시드 값)을 설정해야 한다.

`srand()` 함수는 `unsigned int` 타입의 인자 하나를 받아들인다. 이 인자는 난수 생성기의 초기값으로 사용된다.

예를 들어:
```c
srand(100);
printf("%d\n", rand());  // 동일한 시드 값으로 동일한 결과가 출력된다.
```

프로그램이 매번 다른 난수 시퀀스를 생성하기 원한다면, 프로그램 실행 시간을 기반으로 `srand()` 함수의 시드 값을 설정하는 것이 일반적이다. 이를 위해 `time()` 함수를 사용하곤 한다:
```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

int main() {
    srand((unsigned)time(NULL));
    printf("%d\n", rand());
    return 0;
}
```

이렇게 하면 프로그램을 실행할 때마다 다른 난수 시퀀스가 생성된다.