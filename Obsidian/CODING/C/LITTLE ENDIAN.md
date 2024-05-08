## pointer의 형변환
___
int pointer를 형변환했다.

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
  int *pointer = (int *)malloc(sizeof(int));
  *pointer = 0x12345678; //만약에 0x1234567이면 67 45 23 1이 출력됨
  printf("%x\n", *pointer);
  char *pointer2 = (char *)pointer;
  for (int i = 0; i < 4; i++)
  {
    printf("%x\n", *pointer2);
    pointer2++;
  }
  free(pointer);
}
```
원래는 리틀엔디안도 엄청 헷갈렸는데 이제는 이해해버렸다.

## 배열을 포인터로 사용해 함수로 보내기
___
```c
#include <stdio.h>
void show_arr(int (*ptr)[4], int a);

int main()
{
  int arr1[2][4] = {1, 2, 3, 4, 5, 6, 7, 8};
  int arr2[3][4] = {{10}, {20}, {30}};
  show_arr(arr1, 2);
  show_arr(arr2, 3);
  return 0;
}
void show_arr(int (*ptr)[4], int a)
{
  int i, j;
  printf("----Start Print----\n");
  for (i = 0; i < a; i++)
  {
    for (j = 0; j < 4; j++)
      printf("%d ", ptr[i][j]);
    printf("\n");
  }
}
```
*(ptr)[4]가 가능할 줄 알았는데 불가능했다.

## char str[]
___
```c
char str[] = "Hello";
```
의 경우 마지막에 \0이 생략되어 있다. \0이 포함되어 있지 않으면 print할 때 어디가 끝인지 모르기 때문이다.