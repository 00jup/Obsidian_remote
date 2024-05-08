[[INT_MAX]]
[[void main()]]
[[Pointer 할당 및 해제]]
[[LITTLE ENDIAN]]
[[gcc & g++]]
[[man command]]
[[2의 보수법]]
[[int array의 length 구하기]]
[[최대공약수 구하는 알고리즘]]
[[for을 사용하다가 나온 실수]]
[[srand(time(NULL))을 사용하려면?]]
[[printf]]
[[print_array 함수 const를 쓰는 습관 가지기]]

[[goto]]
[[증감연산자를 이용한 사악한 문제]]


//printf(num); <- c에서 이런 거 하지마셈
C에서는 long 사용함
```c
#include <stdio.h>

int main()
{
    printf("double double size %lu\n", sizeof(long double));
    printf("double double size %lu\n", sizeof(double));
}

// printf(num); <- c에서 이런 거 하지마셈
```
왜 double 이랑 long double 둘다 8이지?

문제가 생겼을 때 원인을 찾아주는 것도 중요한 프로그래밍 능력임.
-> 오버플로우는 오버플로우라고 에러가 나지 않는다.

![[Pasted image 20230921155558.png]]
이해하기 쉽도록 이런 것을 사용하면 좋다. `EXCHANGE_RATE`


코드가 이상하면 .20으로 소수점 자리까지 찍어보기


초기화 해야 하는 경우
```c
int x, y, z, sum;

sum = x + y + z;
sum = 0 //이거 해야 함.
```
sum = 0 잊지 말기.