```python
list = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

with open("test.csv", "w") as f:
    for row in list:
        f.write(f"{row[0],row[1],row[2]}\n")

with open("test.csv", "r") as f:
    # print(f.read()) 이것도 안 좋은 습관이 될 수 있다.
    output = f.readline()
    while output:
        print(output, end="")
        output = f.readline()

```

여기서 output의 의미?

이건 내가 너무 많이 찾아봐서 정리한다.
## if(A)
___
`if(A)`의 경우에는 if(A) 만약 A라면으로 이해했다. 
`if(A)`의 경우 `if(A != 0)`과 같다.
> 즉, A가 false가 아니라면 성립한다는 것 

```c
#include <stdio.h>

int main()
{
  int A, B, C;
  A = 3;
  if (!A)
  {
    printf("A is false\n");
  }
  if (A)
  {
    printf("A is true\n");
  }
}
```
> 결과 `A is true`

## if(!A)
`if(!A)`의 경우에도 A가 false라면으로 이해했다.
`if(!A)`는 `if(A == 0)`과 같다.
>즉, A가 false여야 성립한다. A가 -> `0`이다.

```c
#include <stdio.h>

int main()
{
  int A, B, C;
  A = 0;
  if (!A)
  {
    printf("A is false\n");
  }
  if (A)
  {
    printf("A is true\n");
  }
}
```
> 결과 `A is false`