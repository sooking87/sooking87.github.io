---
title: "[데이터 구조 3번] Expression Stack using Array."
excerpt: "[데이터 구조 3번] Expression Stack using Array."
categories: [Algorithm C_C++]
tags: [Algorithm Study, C/C++, Algorithm]
toc: true
toc_sticky: true
---

## 문제

배열을 사용해서 중위 표기식을 후위 표기식으로 변경하여 계산하기

## 풀이

```c++
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <math.h>
#define STACK_SIZE 100

int isEmpty(int *top)
{
    if (*top == -1) // top이 바뀌어도 수정할 필요 없음
    {
        return 1;
    }
    else
        return 0;
}

int isFull(int *top)
{
    if (*top >= STACK_SIZE) // top이 바뀌어도 수정할 필요 없음
    {
        return 1;
    }
    else
        return 0;
}

void push(char stack[], int *top, int item)
{
    if (isFull(top) == 1)
    {
        printf("Stack is FULL\n");
        exit(1);
    }
    stack[++(*top)] = item;
}

// -> ok
int pop(char stack[], int *top)
{
    int data;
    if (isEmpty(top) == 1)
    {
        printf("Stack is EMPTY\n");
        exit(1);
    }
    data = stack[(*top)--];
    return data;
}

int peek(char stack[], int *top)
{
    if (isEmpty(top) == 1)
    {
        printf("Stack is Empty\n");
        exit(1);
    }
    else
    {
        return stack[*top];
    }
}

// 스택 내 우선순위
int operator(char op)
{
    switch (op)
    {
    case '(':
    case ')':
        return 0;
    case '+':
    case '-':
        return 1;
    case '*':
    case '/':
        return 2;
    case '^':
        return 3;
    }
    return -1;
}

void infix_to_postfix(char exp[], char str[])
{
    int i = 0;
    int strTopIndex = 0;   // 스택 str의 top 인덱스
    char ch, opTopElement; // 스택 op의 top 요소
    int opTopIndex = -1;   // 스택 op의 top 인덱스
    int len = strlen(exp);
    char op[100] = {'\0'}; // 연산자를 임시로 넣어놓을 스택

    for (i = 0; i < len; i++)
    {
        ch = exp[i];

        switch (ch)
        {
        case '+':
        case '-':
        case '*':
        case '/':
        case '^':
            while (!isEmpty(&opTopIndex) && (operator(ch) <= operator(peek(op, &opTopIndex)))) // 연산자 우선순위가 작으면 stack에 ch가 들어가야됨 -> 스택에 있는 연산자를 빼고, ch를 삽입
            {
                str[strTopIndex++] = pop(op, &opTopIndex);
            }

            push(op, &opTopIndex, ch);
            break;
        case '(':
            push(op, &opTopIndex, ch);
            break;
        case ')':
            opTopElement = pop(op, &opTopIndex);
            while (opTopElement != '(')
            {
                str[strTopIndex++] = opTopElement;
                opTopElement = pop(op, &opTopIndex);
            }
            break;
        // 숫자인 경우
        default:
            str[strTopIndex++] = ch;
            break;
        }
    }
    // 연산자 스택인 op에 남아있는 모든 연산자를 str로 옮겨줍니다.
    while (!isEmpty(&opTopIndex))
    {
        str[strTopIndex++] = pop(op, &opTopIndex);
    }
}

int Calculate(char exp[])
{
    char ch;
    int num;                // operand를 저장하기 위한 임시 변수
    int operand1, operand2; // 연산자가 나타났을 경우 pop한 두 피연산자를 넣을 임시 변수
    int result;
    int calTopIndex = -1;   // 스택 cal의 top 인덱스
    char cal[100] = {'\0'}; // 후위 표기식을 계산하기 위한 스택
    for (int i = 0; i < strlen(exp); i++)
    {
        ch = exp[i];
        if (ch != '+' && ch != '-' && ch != '*' && ch != '/' && ch != '^')
        {
            num = ch - '0'; // int형으로 변환
            push(cal, &calTopIndex, num);
        }
        else
        {
            operand2 = pop(cal, &calTopIndex);
            operand1 = pop(cal, &calTopIndex);
            switch (ch)
            {
            case '+':
                result = operand1 + operand2;
                break;
            case '-':
                result = operand1 - operand2;
                break;
            case '*':
                result = operand1 * operand2;
                break;
            case '/':
                result = operand1 / operand2;
                break;
            case '^':
                result = (int)pow(operand1, operand2);
                break;
            }
            push(cal, &calTopIndex, result);
        }
    }
    return pop(cal, &calTopIndex);
}

int main()
{
    printf("I am Sohn Soo Kyoung\n");
    printf("This Project is No_3 :: Expression Stack using Array.\n");
    printf("Please Cheer Up ! Until 2022.05.23\n\n");

    char *data; // 입력 받을 infix를 넣을 변수
    data = (char *)malloc(sizeof(char) * 100);

    char str[100] = {0}; // postifx가 그대로 들어가 있음
    printf("계산할 연산식을 입력해주세요.: ");
    gets(data);

    infix_to_postfix(data, str);
    printf("\nPostfix: %s\n", str);
    int result = Calculate(str);
    printf("%s = %d\n", data, result);
    free(data);
}
```

## 풀이 과정

입력받은 중위 표기식을 후위 표기식으로 바꾸어 줍니다. (infix_to_postfix()) 그후 후위 표기식을 가지고 Calculate()를 사용하여서 계산합니다. <br> <br>

함수 설명 <br>

- int isEmpty(int \*top) : 배열이 비었는지 비어있지 않은지를 판별해줍니다.
- int isFull(int \*top) : 배열이 꽉 찼는지 아닌지를 판별해줍니다.
- void push(char stack[], int *top, int item) : stack의 *top을 1 증가하고 그 위치에 item을 추가해줍니다. **어떤 스택**의 top부분에 item을 추가할 지 정할 수 있습니다.
- int pop(char stack[], int \*top) : stack의 top에 있는 요소를 빼고, top은 1 감소시킵니다. 빠진 data를 리턴을 합니다. **어떤 스택**의 top부분을 pop할 것인지를 정할 수 있습니다.
- int peek(char stack[], int \*top) : stack의 top에 있는 원소를 리턴합니다. (스택 내의 제일 윗 부분에 있는 원소를 확인합니다. ) 어떤 스택의 top부분을 peek할 것인지를 정할 수 있습니다.
- int operator(char op) : op에 대한 스택 내 우선순위를 리턴합니다.
- void infix_to_postfix(char exp[], char str[]) : 중위 표기식(입력 받은 값)인 exp를 후위 표기식으로 바꾸어 배열 str에 넣어줍니다.
- int Calculate(char exp[]) : 후위 표기식으로 바뀐 exp를 계산해주는 함수입니다.
  <br> <br>

주요 변수 및 배열 설명 <br>

- char\* data : 입력받은 infix 수식
- int strTopIndex : postfix가 들어가있는 배열의 top을 가리키는 변수
- char str[100] : postfix가 들어가 있는 스택
- int opTopIndex, opTopElement : 스택 op의 top 인덱스, 요소
- char op[100] : infix_to_postfix 과정에서 연산자를 임시로 넣어 놓을 스택
- int calTopIndex : 스택 cal의 top 인덱스
- char cal[100] : 후위 표기식을 연산하는 과정에서 쓰이는 스택
