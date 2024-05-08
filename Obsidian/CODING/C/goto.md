```c
#include <stdio.h>

int main()
{
    int a = 10;

LOOP:
    do
    {
        if (a == 15)
        {
            a = a + 1;
            goto LOOP;
        }
        printf("a의 값: %d\n", a);
        a++;
    } while (a < 20);

    return 0;
}
```















위에서는 15라는 값을 출력하지 않는다.!!