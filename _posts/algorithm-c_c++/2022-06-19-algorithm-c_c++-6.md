---
title: "[데이터 구조 6번] Doubly Circular Linked List for Escaping Island."
excerpt: "[데이터 구조 6번] Doubly Circular Linked List for Escaping Island."
categories: [Algorithm C_C++]
tags: [Algorithm Study, C/C++, Algorithm]
toc: true
toc_sticky: true
---

## 문제

5번의 문제를 **이중 원형 연결 리스트** 를 이용해서 풀기

## 풀이

```c++
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>
#define LENGTH 11

typedef struct data
{
    int num;
    char name[20];
} element;

typedef struct Node
{
    element data;
    struct Node *llink;
    struct Node *rlink;
} Node;

typedef struct Header
{
    int length; // addLast, delete 메소드를 정의할 때 편의성을 위해서 넣었습니다.
    Node *crnt; // current의 약자로 현재 가리키고 있는 노드를 의미합니다.
    Node *head; // 첫 번째 노드를 가리킵니다.
} DoublyCircularLL;

DoublyCircularLL *createList()
{
    DoublyCircularLL *H;
    H = (DoublyCircularLL *)malloc(sizeof(DoublyCircularLL));
    H->length = 0;
    H->crnt = (Node *)malloc(sizeof(Node));
    H->head = (Node *)malloc(sizeof(Node));
    H->crnt = NULL;
    H->head = NULL;
    return H;
}

int isEmpty(DoublyCircularLL *list)
{
    return (list->head == NULL);
}

void addLast(DoublyCircularLL *list, element *item)
{
    Node *newNode = (Node *)malloc(sizeof(Node));

    if (newNode == NULL)
    {
        fprintf(stderr, "메모리 할당 에러\n");
        exit(1);
    }

    /* 데이터 넣기 */
    newNode->data.num = item->num;
    strcpy(newNode->data.name, item->name);

    if (isEmpty(list)) // 첫 노드라면 -> 헤더 노드를 원형 리스트 순환에서 제외시키기 위해서
    {
        list->head = newNode;
        list->crnt = newNode;
        newNode->rlink = newNode;
        newNode->llink = newNode;
    }
    else
    {
        newNode->llink = list->crnt;
        newNode->rlink = list->head; // newNode를 첫 번째 노드에 오른쪽 방향으로 연결
        list->head->llink = newNode; // list->head : 첫 번째 노드
        list->crnt->rlink = newNode;
        list->crnt = newNode;
    }

    list->length++;
}

element *delete (DoublyCircularLL *list)
{
    if (isEmpty(list))
    {
        printf("List is EMPTY\n");
        exit(1);
    }

    else
    {
        Node *remove = list->crnt;
        element *returnData = &(remove->data);
        Node *prev = list->crnt->llink;
        if (remove == list->head)
        {
            list->head = remove->rlink;
        }
        list->crnt = remove->rlink;
        remove->llink->rlink = remove->rlink;
        remove->rlink->llink = remove->llink;
        list->length--;
        // free(remove);
        return returnData;
    }
}

element *moveCrntR(DoublyCircularLL *list, int skipNum)
{
    Node *ptr = list->crnt;
    for (int i = 0; i < skipNum; i++)
    {
        ptr = ptr->rlink;
    }
    list->crnt = ptr;
    element *returnNode = delete (list);
    return returnNode;
}

element *moveCrntL(DoublyCircularLL *list, int skipNum)
{
    Node *ptr = list->crnt;
    for (int i = 0; i < skipNum; i++)
    {
        ptr = ptr->llink;
    }
    list->crnt = ptr;
    element *returnNode = delete (list);
    return returnNode;
}

int main()
{
    printf("I am Sohn Soo Kyoung\n");
    printf("This Project is No_6 :: Doubly Circular Linked List for Escaping Island.\n");
    printf("Please Cheer Up ! Until 2022.05.23\n\n");

    char *names[20] = {
        "SohnSooKyoung",
        "Park",
        "Kim",
        "Song",
        "Yee",
        "Choi",
        "Jeong",
        "Alice",
        "Clara",
        "Alex",
        "Mia",
    };

    element *item;
    DoublyCircularLL *pplList = createList();
    for (int i = 1; i <= LENGTH; i++)
    {
        item = (element *)malloc(sizeof(element));
        item->num = i;
        strcpy(item->name, names[i - 1]);
        addLast(pplList, item);
    }
    // 시작이 1부터라고 가정
    pplList->crnt = pplList->crnt->rlink;
    srand(time(NULL));
    // int skipNum = rand() % 9 + 1;
    int skipNum = 3;
    printf("skipNum = %d\n", skipNum);
    DoublyCircularLL *loser = createList();

    // *순방향으로 이동한 경우 - 탈락자 및 생존자 출력
    while (pplList->length > 3)
    {
        element *test = moveCrntR(pplList, skipNum);
        addLast(loser, test);
        printf("\n탈락자 명단 \n");
        Node *temp = loser->head;
        while (temp->rlink != loser->head)
        {
            printf("%d %s \n", temp->data.num, temp->data.name);
            temp = temp->rlink;
        }
        printf("%d %s \n", temp->data.num, temp->data.name);

        printf("\n생존자 명단 \n");
        Node *temp2 = pplList->head;
        while (temp2->rlink != pplList->head)
        {
            printf("%d %s \n", temp2->data.num, temp2->data.name);
            temp2 = temp2->rlink;
        }
        printf("%d %s \n", temp2->data.num, temp2->data.name);
    }

    // *순방향으로 이동한 경우
    printf("\n순방향으로 이동한 경우\n");
    while (pplList->length > 3)
    {
        moveCrntR(pplList, skipNum);
    }

    Node *finalListR = pplList->head;
    printf("배를 타고 무인도를 탈출할 최종 3인은 ");
    for (int i = 0; i < 3; i++)
    {
        if (i == 2)
        {
            printf("%d번 %s 님 입니다. ^^\n", finalListR->data.num, finalListR->data.name);
        }
        else
        {
            printf("%d번 %s 님, ", finalListR->data.num, finalListR->data.name);
        }
        finalListR = finalListR->rlink;
    }


    while (pplList->length > 3)
    {
        element *test = moveCrntL(pplList, skipNum);
        addLast(loser, test);
        printf("\n탈락자 명단 \n");
        Node *temp = loser->head;
        while (temp->rlink != loser->head)
        {
            printf("%d %s \n", temp->data.num, temp->data.name);
            temp = temp->rlink;
        }
        printf("%d %s \n", temp->data.num, temp->data.name);

        printf("\n생존자 명단 \n");
        Node *temp2 = pplList->head;
        while (temp2->rlink != pplList->head)
        {
            printf("%d %s \n", temp2->data.num, temp2->data.name);
            temp2 = temp2->rlink;
        }
        printf("%d %s \n", temp2->data.num, temp2->data.name);
    }

    // *역방향으로 이동한 경우
    printf("역방향으로 이동한 경우\n");
    while (pplList->length > 3)
    {
        moveCrntL(pplList, skipNum);
    }

    Node *finalListL = pplList->head;
    printf("배를 타고 무인도를 탈출할 최종 3인은 ");
    for (int i = 0; i < 3; i++)
    {
        if (i == 2)
        {
            printf("%d번 %s 님 입니다. ^^\n", finalListL->data.num, finalListL->data.name);
        }
        else
        {
            printf("%d번 %s 님, ", finalListL->data.num, finalListL->data.name);
        }
        finalListL = finalListL->rlink;
    }
}
```

## 풀이 과정

1. addLast()를 통해서 사람의 데이터를 pplList에 넣어줍니다.
2. 순방향 출력을 위해서라면 pplList의 길이가 3이 되기 전까지 moveCrntR()을 통해서 skipNum 만큼 crnt를 이동시키면서 해당 노드를 지워줍니다.
3. 역방향 출력을 위해서라면 pplList의 길이가 3이 되기 전까지 moveCrntL()을 통해서 skipNum 만큼 crnt를 이동시키면서 해당 노드를 지워줍니다.
4. 탈락자가 발생할 때마다, 탈락자와 생존자의 명단을 출력하였습니다. (문제 5_C 항목)
5. 3명의 데이터를 출력해줍니다. <br> <br>

함수 설명 <br>

- DoublyCircularLL \*createList() : 처음 새로운 원형 연결 리스트를 만들 때 사용됩니다. 헤더 노드의 메모리를 할당 받고, 헤더 노드를 구성하고 있는 length는 0으로, crnt, head를 NULL로 초기화 시켜주는 역할을 합니다.
- int isEmpty(DoublyCircularLL \*list) : 리스트가 비어있는 노드인지 아닌지를 판별해줍니다. list->head == NULL 조건이 참이라면 빈 리스트라는 의미로 1을 리턴하고, 그렇지 않다면 0을 리턴합니다.
- void addLast(DoublyCircularLL *list, element *item) : 마지막 노드 뒤에 새로운 노드를 추가해줍니다. 그때의 노드는 item 데이터를 가지고 있습니다.
- element *delete(DoublyCircularLL *list) : list에서 list->crnt를 지워주는 함수입니다.
- moveCrntR() / moveCrntL() 은 pplList->crnt를 이동시켜서 지울 노드를 가리키도록 하는 함수는 맞습니다. 하지만 문제에서 순방향으로 출력시키고, 역방향으로 출력시키라고 하였으므로 두 개로 분리하여서 순방향으로 출력시키기 위해서는 moveCrntR()를 통해서 crnt를 이동시키고, 역방향으로 출력시키기 위해서는 moveCrntL()을 통해서 crnt를 이동시킵니다. <br> <br>

변수 설명 <br>

- element 구조체 : 숫자와 사람 이름을 넣기 위해서 만들었습니다 element는 노드의 data부분에 해당합니다.
- Node 구조체 : 하나의 노드이며 노드 안에는 data와 rllink와 llink를 구성하고 있습니다.
- DoublyCircularLL 구조체 : pplList의 시작 부분을 의미하고, 헤더 노드를 가지고 있습니다.
  헤더 노드에는 length, crnt, head가 있습니다. length는 리스트의 길이를 가지고 있습니다. crnt는 current의 약자로 현재 가리키고 있는 노드를 뜻합니다. 추가될 때마다 crnt는 한 칸씩 뒤로 이동하며, 지울 노드를 가리키는 데에 사용됩니다. head는 가장 첫 번째 노드를 가리키며, 출력 시 오름차순으로 출력될 수 있도록 합니다.
- pplList : 사람의 데이터를 가지고 있는 이중 원형 연결 리스트의 시작 부분입니다.
- skipNum : 규칙에 따라 탈출하지 못할 사람을 고르기 위한 숫자입니다. #include <time.h>에서 srand(time(NULL))을 사용해서 완벽한 랜덤 함수를 출력할 수 있도록 하였습니다. rand()의 경우는 특정 규칙이 있어 랜덤처럼 보이지만 사실 규칙이 정해져있으므로 srand()를 사용하였습니다.
