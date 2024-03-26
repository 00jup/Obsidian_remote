
# 문제, 1.23을 입력했을 때 오류 없이 정상적으로 출력되도록 printf를 수정하여라
```c
#include<stdio.h>

int main(void){
	 int i;
	 scanf("%f", &i);
	 printf("%d %f\n",i,i);
}
```

이거 보면서 교수님은 이런 예시를 어떻게 찾을까 하는 생각하면서 문제를 풀었다.



```c
#include<stdio.h>

int main(void){
	 int i;
	 scanf("%f", &i);
	 printf("%d %f\n",*(int*)i,*(float*)i);
}
```