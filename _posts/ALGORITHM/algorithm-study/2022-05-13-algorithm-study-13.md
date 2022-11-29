---
title: "[C] Stack"
excerpt: "[C] Stack"
categories: [Algorithm Study]
tags: [Algorithm Study, C, Algorithm]
toc: true
toc_sticky: true
published: true
---

## 🔮 배열로 구현

```c
#include <stdio.h>
#define STACK_SIZE 100

/* 1차원 배열을 이용한 stack 구현 */

typedef int element; // element를 int 타입으로 정의
element stack[STACK_SIZE];

void push(int *top, element item)
{
    if (*top >= STACK_SIZE - 1)
    {
        printf("Stack if FULL\n");
        return;
    }
    stack[++(*top)] = item;
}

element pop(int *top)
{
    if (*top == 01)
    {
        printf("Stack is EMPTY\n");
        exit(1);
    }
    else
        return stack[(*top)--];
}

int isEmpty(int *top)
{
    if (*top == -1)
        return 1;
    else
        return 0;
}

void delete (int *top)
{
    if (top == -1)
    {
        printf("Stack is empty\n");
        exit(1);
    }
    else
        (*top)--;
}

element peek(int top)
{
    if (top == -1)
    {
        printf("Stack is EMPTY\n");
        exit(1);
    }
    else
        return stack[top];
}

int main()
{
    int top = -1;
    element data1, data2;
    printf("push data1: %d\n", 1);
    push(&top, 1);
    printf("push data 2: %d\n", 2);
    push(&top, 2);
    data2 = peek(top);
    printf("peek data2: %d\n", data2);
    delete (&top);
    printf("delete data2\n");
    data1 = pop(&top);
    printf("pop data1: %d\n", data1);
    return 0;
}

>>>
push data1: 1
push data 2: 2
peek data2: 2
delete data2
pop data1: 1
```

## 🔮 연결리스트로 구현

```c
#include <stdio.h>
#include <string.h>
#include <stdlib.H>

typedef struct
{
    int id;
    char name[10];
    char grade;
} element;

typedef struct stackNode
{
    element data;
    struct stackNode *link;
} stackNode;

void push(stackNode **top, element data)
{
    stackNode *temp;
    temp = (stackNode *)malloc(sizeof(stackNode));
    temp->data = data;
    temp->link = *top;
    *top = temp;
}

element pop(stackNode **top)
{
    stackNode *temp;
    element data;
    temp = *top;
    if (temp == NULL)
    {
        printf("Stack is EMPTY\n");
        exit(1);
    }
    else
    {
        data = temp->data;
        *top = temp->link;
        free(temp);
        return data;
    }
}

element peek(stackNode *top)
{
    element data;
    if (top == NULL)
    {
        printf("Stack is EMPTY\n");
        exit(1);
    }
    else
    {
        data = top->data;
        return data;
    }
}

void delete (stackNode **top)
{
    stackNode *temp;
    if (*top == NULL)
    {
        printf("Stack is EMPTY\n");
        exit(1);
    }
    else
    {
        temp = *top;
        *top = (*top)->link;
        free(temp);
    }
}

int main()
{
    stackNode *top = NULL;
    element data1, data2, data3, data4;

    data1.id = 1;
    strcpy(data1.name, "LEE");
    data1.grade = 'A';

    data2.id = 2;
    strcpy(data2.name, "Park");
    data2.grade = 'B';

    printf("push data1 : (%d, %s, %d)\n", data1.id, data1.name, data1.grade);
    push(&top, data1);

    printf("push data1 : (%d, %s, %d)\n", data2.id, data2.name, data2.grade);
    push(&top, data2);

    data3 = peek(top);
    printf("peek data2 : (%d, %s, %d)\n", data3.id, data3.name, data3.grade);
    delete (&top);
    printf("delete data2\n");
    data4 = pop(&top);
    printf("pop data1 : (%d, %s, %d)\n", data4.id, data4.name, data4.grade);

    return 0;
}

>>>
push data1 : (1, LEE, 65)
push data1 : (2, Park, 66)
peek data2 : (2, Park, 66)
delete data2
pop data1 : (1, LEE, 65)
```
