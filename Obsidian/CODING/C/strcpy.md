
```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

int main()
{
    char *p = "Hello1";
    char word[] = "Hello2";
    char *pc;
    pc = word;

    printf("p = %s / p의 주소 %p \n", p, &p);
    printf("word = %s / word의 주소 %p \n", word, &word);

    pc = "bye1";
    strcpy(word, "bye2");
    //strcpy는 여기서 bye2를 넣었는데 word에 있던 게 글자수가 더 작다면 바뀌지 않는다.

    printf("pc = %s / pc의 주소 %p \n", pc, &pc);
    printf("p = %s / p의 주소 %p \n", p, &p);
    printf("word = %s / word의 주소 %p \n", word, &word);

    int *pi = (int *)malloc(sizeof(int));
    *pi = 100;
    // pi = 200;

    printf("pi = %d / pi의 주소 %p \n", *pi, pi);
}
```

strcpy 사용할 때 주의하기!