C 언어에는 Python의 `match-case`에 직접적으로 대응되는 문법이 없습니다. 그러나 `switch-case` 문을 사용하여 유사한 기능을 구현할 수는 있습니다. 단, `switch-case`는 정수형 데이터에만 적용될 수 있고, 문자열이나 소수점, 복잡한 데이터 타입에는 적용할 수 없습니다.

아래에 C 언어의 `switch-case` 예시를 몇 개 들겠습니다.

## 기본 사용법

```c
switch (expression) {
    case constant1:
        // code to be executed;
        break;
    case constant2:
        // code to be executed;
        break;
    default:
        // code to be executed if expression doesn't match any constant;
}
```

## 정수형 예시

```c
int num = 2;

switch (num) {
    case 0:
        printf("zero\n");
        break;
    case 1:
        printf("one\n");
        break;
    case 2:
        printf("two\n");
        break;
    default:
        printf("number is greater than two\n");
}
```

## 문자 예시

```c
char grade = 'A';

switch (grade) {
    case 'A':
        printf("Excellent\n");
        break;
    case 'B':
        printf("Good\n");
        break;
    default:
        printf("Grade unavailable\n");
}
```

`switch-case` 문의 제약 사항을 극복하려면 `if-else if-else` 체인을 사용해야 할 수도 있습니다. 이는 문자열이나 소수점, 복잡한 데이터 타입을 다루는 데 더 유연합니다.

## 문자열을 사용한 if-else 예시

```c
char *language = "English";

if (strcmp(language, "English") == 0) {
    printf("Hello\n");
} else if (strcmp(language, "Spanish") == 0) {
    printf("Hola\n");
} else {
    printf("Unknown language\n");
}
```

C 언어의 `switch-case`는 Python의 `match-case`보다 덜 유연하지만, 여전히 특정 조건에는 유용하게 사용될 수 있습니다.

[[불가능한 예시들]]
