```c
#include <stdio.h>
#include <stdlib.h>

#define MAX 10

struct contact
{
    int number;
    char name[MAX];
    int phone;
} typedef CONTACT;

int main(void)
{

    CONTACT *person;
    int N;
    printf("N 입력 : ");
    scanf("%d", &N);
    getchar();
    person = (CONTACT *)malloc(sizeof(CONTACT) * N);

    for (int i = 0; i < N; i++)
    {
        printf("번호 : ");
        scanf("%d", &person[i].number);
        printf("이름 : ");
        scanf("%s", person[i].name);
        printf("전화번호 :");
        scanf("%d", &person[i].phone);
        while (getchar() != '\n')
            ;

        printf("\n");
    }
    printf("\n");
    for (int i = 0; i < N; i++)
    {
        printf("이름 : %s\n", person[i].name);
        printf("번호 : %d\n", person[i].number);
        printf("전화번호 : %d\n", person[i].phone);
    }
}

```


