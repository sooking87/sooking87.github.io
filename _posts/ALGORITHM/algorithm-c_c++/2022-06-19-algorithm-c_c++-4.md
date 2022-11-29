---
title: "[데이터 구조 4번] Expression Stack using Linked List."
excerpt: "[데이터 구조 4번] Expression Stack using Linked List."
categories: [Algorithm C_C++]
tags: [Algorithm Study, C/C++, Algorithm]
toc: true
toc_sticky: true
---

## 문제

연결 리스트를 사용해서 중위 표기식을 후위 표기식으로 변경하여 계산하기

## 풀이

```c++
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <math.h>

typedef struct stackNode
{
    int data;
    struct stackNode *llink;
    struct stackNode *rlink;
} Node;

typedef struct Header
{
    int length;
    Node *top;
    Node *tail;
} linkedList;

linkedList *createStack()
{
    linkedList *H;
    H = (linkedList *)malloc(sizeof(linkedList));
    H->length = 0;
    H->top = NULL;
    H->tail = NULL;
    return H;
}

int isEmpty(linkedList *stack)
{
    return (stack->tail == NULL);
}

void push(linkedList *stack, int data)
{
    Node *newNode = (Node *)malloc(sizeof(Node));
    if (newNode == NULL)
    {
        fprintf(stderr, "메모리 할당 에러\n");
        exit(1);
    }
    newNode->data = data; // data 넣고
    newNode->rlink = stack->top; // 첫 노드의 rlink = NULL로 첫 노드가 아니면 top이 가리키던 노드를 가리킴
    stack->top = newNode;        // top을 새로운 노드에 연결

    if (isEmpty(stack)) // 첫 노드 push라면
    {
        newNode->llink = stack->tail;
        stack->tail = newNode;
    }
    else // 첫 노드가 아니라면
    {
        newNode->rlink->llink = newNode;
        newNode->llink = NULL;
    }
    stack->length++;
}

int pop(linkedList *stack)
{
    if (isEmpty(stack))
    {
        printf("Stack is EMPTY\n");
        exit(1);
    }
    else
    {
        Node *remove = stack->top;
        int data = remove->data;
        stack->top = remove->rlink;
        // stack의 길이가 1이 아니면 remove의 llink는 NULL로 만들어준다.
        if (stack->length != 1)
        {
            stack->top->llink = NULL; // 지울 노드를 가리키던 링크
        }
        // stack의 길이가 1이라는 것은 pop하면 stack에 남아있는 노드가 없으므로 스택 초기화 시키고(NULL) 바로 data 리턴
        else
        {
            stack->top = NULL;
            stack->tail = NULL;
        }
        stack->length--;
        free(remove);
        return data;
    }
}

int peek(linkedList *stack)
{
    if (isEmpty(stack))
    {
        printf("Stack is EMPTY\n");
        exit(1);
    }
    else
    {
        return stack->top->data;
    }
}

// 스택 내 우선순의
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

void infix_to_postfix(char exp[], linkedList *str)
{
    int i = 0;
    char ch, opTopElement; // 스택 op의 top 요소
    int len = strlen(exp);
    linkedList *op = createStack();

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
            while (!isEmpty(op) && (operator(ch) <= operator(peek(op))))
            {
                push(str, pop(op));
            }
            push(op, ch);
            break;
        case '(':
            push(op, ch);
            break;
        case ')':
            opTopElement = pop(op);
            while (opTopElement != '(')
            {
                push(str, opTopElement);
                opTopElement = pop(op);
            }
            break;
        default:
            push(str, ch);
            break;
        }
    }
    while (!isEmpty(op))
    {
        push(str, pop(op));
    }
}

int Calculate(linkedList *str)
{
    char ch;
    int num;                // operand를 저장하기 위한 임시 변수
    int operand1, operand2; // 연산자가 나타났을 경우 pop한 두 피연산자를 넣을 임시 변수
    int result;
    linkedList *cal = createStack(); // 후위 표기식을 계산하기 위한 스택
    Node *ptr = str->tail;

    for (int i = 0; i < str->length; i++)
    {
        ch = ptr->data;
        if (ch != '+' && ch != '-' && ch != '*' && ch != '/' && ch != '^')
        {
            num = ch - '0'; // int형으로 변환
            push(cal, num);
        }
        else
        {
            operand2 = pop(cal);
            operand1 = pop(cal);
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
            push(cal, result);
        }
        ptr = ptr->llink;
    }
    return pop(cal);
}

int main()
{
    printf("I am Sohn Soo Kyoung\n");
    printf("This Project is No_4 :: Expression Stack using Linked List.\n");
    printf("Please Cheer Up ! Until 2022.05.23\n\n");

    char *data; // 입력받은 infix 수식
    data = (char *)malloc(sizeof(char) * 100);
    linkedList *str; // postfix가 들어가있는 스택
    str = createStack();

    printf("계산할 연산식을 입력해주세요.: ");
    gets(data);

    infix_to_postfix(data, str);
    int result = Calculate(str);
    printf("%s = %d\n", data, result);
}
```

## 풀이 과정

입력받은 중위 표기식을 후위 표기식으로 바꾸어 줍니다. (infix_to_postfix()) 그 후, 후위 표기식을 가지고 Calculate()를 사용하여서 계산합니다. <br> <br>

함수 설명 <br>

- linkedList \*createStack() : 새로운 스택을 만들어줌과 동시에 해더 노드를 초기화 시켜 줍니다.
- int isEmpty(int \*top) : 스택이 비었는지 비어있지 않은지를 판별해줍니다.
- void push(linkedList \*stack, int data) : stack에 data를 넣어줍니다.
- int pop(linkedList \*stack) : stack의 top 부분을 제거합니다. 하지만 free()를 통해서 동적 메모리 할당을 해제 시켜버리면 다른 스택에서 사용될 값이 사라질 수 있으므로 연결만 끊는 식으로 pop()을 만들었습니다.
- int peek(linkedList \*stack) : stack의 top에 있는 원소를 리턴합니다. (스택 내의 제일 윗 부분에 있는 원소를 확인합니다.
- int operator(char op) : op에 대한 스택 내 우선순위를 리턴합니다.
- void infix_to_postfix(char exp[], linkedList \*str) : 중위 표기식(입력 받은 값)인 exp를 후위 표기식으로 바꾸어 스택 str에 넣어줍니다.
- int Calculate(linkedList \*str) : 후위 표기식으로 바뀐 exp를 계산해주는 함수입니다. <br> <br>

주요 변수 및 배열 설명 <br>

- char \*data : 입력받은 infix 수식

- linkedList\* str : postfix가 들어가는 스택
- linkedList\* op : infix_to_postfix 과정에서 연산자를 임시로 넣어 놓을 스택
- linkedList\* cal : 후위 표기식을 연산하는 과정에서 쓰이는 스택
