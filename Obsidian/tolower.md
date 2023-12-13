
```c
#include <stdio.h>
#include <string.h>
#include <ctype.h>

int main()
{
    char words[] = "Hello";
    for (int i = 0; words[i] != NULL; i++)
    {
        printf("%c", words[i]);
        words[i] = tolower(words[i]);
        printf("%c\n", words[i]);
    }
}
```

tolower를 사용하려면 <ctype.h>가 포함되어야 한다.

	그리고 tolower(words[i])
	만 사용하고 끝낼 것이 아니라, words[i] = tolower(words[i])로 설정해줘야 한다.
	