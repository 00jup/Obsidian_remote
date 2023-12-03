Pointer로 배열을 보낼 때는 size를 따로 보내야 함

```c
#include <stdio.h>

void print_array(int *array, int size)
{
    for (int i = 0; i < size; i++)
    {
        printf("%d ", *(array + i));
    }
    printf("\n");
}

void array_copy(int a[], int b[], int size)
{
    for (int i = 0; i < size; i++)
    {
        b[i] = a[i];
    }
}

int main()
{
    int A[] = {5, 19, 20, 23, 44};

    print_array(A, sizeof(A) / sizeof(A[0]));
    int B[sizeof(A) / sizeof(A[0])] = {};
    array_copy(A, B, sizeof(A) / sizeof(A[0]));
    print_array(B, sizeof(B) / sizeof(B[0]));
}
```

## 실수 1
여기서 print_array함수를 만들 때 size를 안 보내고 함수 안에서 sizeof(array) / sizeof(array[0])로 size를 바로 얻으려고 했다.

근데 여기서 array는 포인터이므로 그냥 주소 자체라서 불가능하다.

그래서 size를 정해줘야 한다!!

## 실수 2
B라는 array를 만든다고 했을 때 B array의 size를 정해줘야 한다.
이건 python이 아니다.

아니면 `동적할당 하든지`
