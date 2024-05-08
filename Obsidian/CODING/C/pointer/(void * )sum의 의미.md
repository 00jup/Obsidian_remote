
c에서 함수를 살펴보다보면 위와 같은 형식의 함수들이 종종 보인다.

과제를 할 때 이 부분을 인지하지 않고 진행했다.
```c
#include <stdio.h>

int sum(char *array, int length)
{
    int result = 0;
    for (int i = 0; i < length; i++)
    {
        result += array[i];
    }

    return result;
}

int main()
{
    int inum[] = {1, 2, 3, 4};
    char cnum[] = {3, 5, 8, 7, 9};

    printf("%d\n", sum((char *)inum, sizeof(inum) / sizeof(int) * 4));
    printf("%d\n", sum(cnum, sizeof(cnum) / sizeof(char)));
    return 0;
}
```

따라서 아래와 같이 수정하면 더 좋을 듯하다.

```c
#include <stdio.h>

int sum((void *)array,int size, int length)
{
    int result = 0;
    switch(size){
	    case 1: for (int i = 0; i < length; i++)
	        result += *(char *) a;
	    case 4: for (int i = 0; i < length; i++)
		    result += *(int *) a;
	    
    }
	    

    return result;
}

int main()
{
    int inum[] = {1, 2, 3, 4};
    char cnum[] = {3, 5, 8, 7, 9};

    printf("%d\n", sum(inum, 4, sizeof(inum) / sizeof(int) * 4));
    printf("%d\n", sum(cnum, 1, sizeof(cnum) / sizeof(char)));
    return 0;
}
```