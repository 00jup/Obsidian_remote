
```c
int *A, *B;
printf("A, B를 입력하세요: ");
scanf("%d %d", A, B);
```

이렇게 하면 안 됨

```c
int *A, *B;

A = (int *)malloc(sizeof(int));
B = (int *)malloc(sizeof(int));

printf("A, B를 입력하세요: ");
scanf("%d %d", A, B);
```

이렇게 해야 함