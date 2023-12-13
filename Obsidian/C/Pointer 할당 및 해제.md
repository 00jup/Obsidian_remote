# 할당 및 해제하는 법

**malloc 쓰려면 ``<stdlib.h>`` 해야함**

```c
#include <stdio.h>
#include <stdlib.h>

int main(void){
	int none_pointer;
	int rows = 5, cols = 3
	
	int *pointer;
	pointer = (int*)malloc(rows * sizeof(int));
	
	
	int **double_pointer;
	double_pointer = (int**)malloc(rows * sizeof(int*));
	for(int i = 0; i < rows; i++)
		double_pointer[i] = (int *)malloc(cols * sizeof(int));


	//pointer
	free(pointer);
	//double_pointer
	for(int i =0; i<rows; i++)
		free(double_pointer[i]);
	free(double_pointer);
	return 0;
}
```
## Q malloc에서 `(int**)` `(int*)`을 쓰는 이유?
ㅑ반환형을 앞에 붙인 것임. 그래서 double_pointer, pointer 반환 시에 각각 (int**) (int*)을 붙인다.

[[Pointer 주소를 저장하는 2가지 방법]]
[[rows and cols]]
[[Pointer 주소 비교]]
[[(void*) 포인터 형인 것을 알려주기 위함]]
[[Pointer로 값을 받으려면 동적할당 해야 함]]

[[Pointer로 배열을 보낼 때는 size를 따로 보내야 한다.]]

[[배열을 pointer의 주소를 이용해서 표현하는 방법]]


[[calloc use]]

[[Pointer에서 주소를 전달한다는 것의 의미 이제 이해함]]
[[string.h]]
