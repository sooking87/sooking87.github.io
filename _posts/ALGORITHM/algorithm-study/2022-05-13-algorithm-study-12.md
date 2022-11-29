---
title: "[C] 헤더 노드를 가진 연결 리스트 / 이중 연결 리스트"
excerpt: "[C] 헤더 노드를 가진 연결 리스트 / 이중 연결 리스트"
categories: [Algorithm Study]
tags: [Algorithm Study, C, Algorithm]
toc: true
toc_sticky: true
published: true
---

### 📍 노드 및 빈리스트 만들기

```c
#include <stdio.h>

/* 단순 연결 리스트 노드 구조 */
typedef struct listNode
{
    char data[5];
    struct listNode *link;
} listNode;

/* 헤더 노드 구조 */
typedef struct
{
    int length;
    listNode *head;
    listNode *tail;
} h_linkedList;

h_linkedList *create_h_linkedList()
{
    h_linkedList *H;
    H = (h_linkedList *)malloc(sizeof(h_linkedList));
    H->length = 0;
    H->head = NULL;
    H->tail = NULL;
    return H;
}
```

### 📍 이중 연결 리스트 노드

```c
#include <stdio.h>

/* 이중 연결 리스트 노드 구조 */
typedef struct doubleListNode
{
    char data[5];
    struct doubleListNode *rlink;
    struct doubleListNode *llink;
} doubleListNode;

typedef struct
{
    int length;
    doubleListNode *head;
} doubleCircularPlus;

doubleCircularPlus *create_doubleCircularPlus()
{
    doubleCircularPlus *H;
    H = (doubleCircularPlus *)malloc(sizeof(doubleCircularPlus));
    H->length = 0;
    H->head = (doubleListNode *)malloc(sizeof(doubleListNode));
    H->head->rlink = H->head;
    H->head->llink = H->head;
    return H;
}
```
