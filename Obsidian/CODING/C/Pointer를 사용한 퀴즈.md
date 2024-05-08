```c
// file : _10_20192294_1.c
// last modified : 2023.11.23. 17:08 by 박정욱

#include <stdio.h>
#include <time.h>
#include <stdlib.h>
#define SIZE 100
#define Problem_Number 10

typedef struct question
{
    char question[SIZE];
    char item1[SIZE];
    char item2[SIZE];
    char item3[SIZE];
    char item4[SIZE];
    int solution;
} QUESTION;

int main()
{
    int select_num;
    // 보기 선택
    int success = 0;
    // 문제 풀이 성공횟수

    QUESTION example[Problem_Number] = {
        {"위의 언어 중에서 임베디드 장치에 가장 적합한 프로그래밍 언어는? ", "1. python", "2. Java", "3. C", "4. Javascript", 3},
        {"1+1은 무엇일까요? ", "1. 1", "2. 2", "3. 3", "4. 4", 2},
        {"김현준 교수님이 가르지는 수업은? ", "1. 기초컴퓨터 프로그래밍", "2. 프로그래밍", "3. AI사고와 디자인적 문제 해결", "4. 인간행동과 심리", 2},
        {"프로그래밍 수업의 시작 시간은? ", "1. 12:00", "2. 13:00", "3. 14:00", "4. 15:00", 4},
        {"11월23일 10주차 강의자료에서 가장 많이 언급된 단어는 무엇일까? ", "1. 구조체", "2. 파이썬", "3. 저급 언어", "4. 고급 언어", 1},
        {"김현준 교수님의 진짜 생일은 무엇인가? ", "1. 2월 27일", "2. 2월 28일", "3. 2월 29일", "4. 4월 10일", 3},
        {"프로그래밍 수업을 들으면서 가장 많이 사용한 언어는 무엇인가? ", "1. python", "2. Java", "3. C", "4. Javascript", 3},
        {"다음 중 공업 수학 2에서 나오지 않는 방정식을 고르시오. ", "1. 열전도 방정식", "2. 파동 방정식", "3. 라플라스 방정식", "4. 슈뢰딩거 방정식", 4},
        {"이 문제를 출제한 사람의 이름은? ", "1. 박정욱", "2. 박상욱", "3. 박창욱", "4. 박성욱", 1},
        {"11월 23일의 강의 주차는 몇 주차일까? ", "1. 9주차", "2. 10주차", "3. 11주차", "4. 12주차", 4}};
    // 문제 생성

    srand(time(NULL));
    int rand_number[10];
    // 난수 초기화 및 난수를 담을 배열 생성

    for (int i = 0; i < Problem_Number; i++)
    {
        rand_number[i] = (rand() % Problem_Number) + 1;
        for (int j = 0; j < i; j++)
            if (rand_number[j] == rand_number[i])
                i--;
    }
    // 동일하지 않은 수 Problem_Number개를 담는다.

    printf("-----------------문제 시작-----------------\n\n");
    for (int i = 0; i < 10; i++)
    {
        printf("%s\t%s\t%s\t%s\t \n\n%s", (example + rand_number[i] - 1)->item1, (example + rand_number[i] - 1)->item2, (example + rand_number[i] - 1)->item3, (example + rand_number[i] - 1)->item4, (example + rand_number[i] - 1)->question);
        // 문제 출력

        // 정답 체크
        scanf("%d", &select_num);
        if (select_num == (example + rand_number[i] - 1)->solution)
        {
            success++;
            printf("--------------\n| 맞았습니다.|\n--------------\n\n");
        }
        else
            printf("--------------\n| 틀렸습니다.|\n--------------\n\n");
    }

    printf("\n모든 %d개의 문제가 끝났습니다. 고생하셨습니다.\n\n스코어 : 정답 %d / 오답 %d\n", Problem_Number, success, Problem_Number - success);

    return 0;
}

