---
title: "[C] Queue"
excerpt: "[C] Queue"
categories: [Algorithm Study]
tags: [Algorithm Study, C, Algorithm]
toc: true
toc_sticky: true
published: true
---

## 🔮 배열로 구현

```c
#define Q_SIZE 100

typedef int element;
element queue[Q_SIZE];

void enqueue(int *rear, element item)
{
    if (*rear == Q_SIZE - 1)
    {
        printf("Queue is full\n");
        return;
    }
    queue[++*rear] = item;
}

int isEmpty(int *front, int rear)
{
    if (*front == rear)
        return 1;
    else
        return 0;
}

element dequeue(int *front, int rear)
{
    if (*front == rear)
    {
        printf("Queue is EMPTY\n");
        exit(1);
    }
    else
        ++*front;
}

element peek(int front, int rear)
{
    if (front == rear)
    {
        printf("Queue is EMPTY\n");
        exit(1);
    }
    else
    {
        return queue[front++];
    }
}

int main()
{
    int front = -1; // 삭제 연산 인덱스
    int rear = -1;  // 삽입 연산 인덱스
    element data;

    enqueue(&rear, 1);
    enqueue(&rear, 2);

    data = peek(front, rear);

    data = dequeue(&front, rear);
    printf("data=%d\n", data);

    data = dequeue(&front, rear);
    printf("data=%d\n", data);

    return 0;
}
```

## 🔮 연결리스트로 구현

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct
{
    int id;
    char name[10];
    char grade;
} element;

typedef struct queueNode
{
    element data;
    struct queueNode *link;
} queueNode;

typedef struct
{
    queueNode *front;
    queueNode *rear;
    int length;
} linkedQueue;

linkedQueue *createQ()
{
    linkedQueue *q;
    q = (linkedQueue *)malloc(sizeof(linkedQueue));
    q->front = NULL;
    q->rear = NULL;
    q->length = 0;
    return q;
}

int isEmpty(linkedQueue *q)
{
    return (q->length == 0);
}

void enqueue(linkedQueue *q, element item)
{
    queueNode *newNode;
    newNode = (queueNode *)malloc(sizeof(queueNode));
    newNode->data = item;
    newNode->link = NULL;
    if (q->length == 0)
    {
        q->front = q->rear = newNode;
    }
    else
    {
        q->rear->link = newNode;
        q->rear = newNode;
    }
    q->length++;
}

element dequeue(linkedQueue *q)
{
    queueNode *temp;
    element item;
    if (q->length == 0)
    {
        printf("Queue is EMPTY\n");
        exit(1);
    }
    else
    {
        item = q->front->data;
        temp = q->front;
        q->front = q->front->link;
        if (q->front == NULL)
            q->rear = NULL;
        q->length--;
        free(temp);
        return item;
    }
}

void delete (linkedQueue *q)
{
    queueNode *temp;
    if (q->length == 0)
    {
        printf("Queue is EMPTY\n");
        exit(1);
    }
    else
    {
        temp = q->front;
        q->front = q->front->link;
        if (q->front == NULL)
            q->rear = NULL;
        q->length--;
        free(temp);
    }
}

element peek(linkedQueue *q)
{
    if (q->length == 0)
    {
        printf("Queue is EMPTY\n");
        exit(1);
    }
    else
        return q->front->data;
}

int main()
{
    element item;
    linkedQueue *q;
    q = createQ();

    item.id = 123;
    strcpy(item.name, "Hong");
    item.grade = 'A';

    enqueue(q, item);
}
```
