

```c
#include <stdio.h>

void set_pointer(char **q);
int main(void)
{
    char *p;
    set_pointer(&p);

    printf("오늘의 격언: %s \n", p);
    return 0;
}

void set_pointer(char **q)
{
    *q = "All that glisters is not gold.";
}
```

여기서 `void set_pointer(char **q)` 를 `char *q` 로 사용하면 복사본을 전달하는 거니까

```c
void set_pointer(char *q)
{
    q = "All that glisters is not gold.";
}
```

만약 이렇게 사용한다면 q의 값이 변하는 거지 p의 값이 변하는 게 아니다!

그래서 주소를 전달해야 하는 거임.

-> 그래야 p의 값을 바꿀 수 있다.

[[Pointer 사용 예제]]
