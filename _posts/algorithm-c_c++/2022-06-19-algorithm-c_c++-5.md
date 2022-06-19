---
title: "[데이터 구조 5번] Singly Circular Linked List for Escaping Island."
excerpt: "[데이터 구조 5번] Singly Circular Linked List for Escaping Island."
categories: [Algorithm C_C++]
tags: [Algorithm Study, C/C++, Algorithm]
toc: true
toc_sticky: true
---

## 문제

11명이 조난되었는데 3명만 탈출을 할 수 있는 배가 있다. 사람들별로 정해진 숫자가 있고, 랜덤으로 숫자를 뽑아서 3명이 남을 때까지 랜덤 숫자대로 카운트하여 해당 사람을 탈락시킨다. **원형 연결 리스트** 를 사용

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
    struct Node *rlink;
} Node;

typedef struct Header
{
    int length; // addLast, delete 메소드를 정의할 때 편의성을 위해서 넣었습니다.
    Node *crnt; // current의 약자로 현재 가리키고 있는 노드를 의미합니다.
    Node *head; // 첫 번째 노드를 가리킵니다.
} SinglyCircularLL;

SinglyCircularLL *createList()
{
    SinglyCircularLL *H;
    H = (SinglyCircularLL *)malloc(sizeof(SinglyCircularLL));
    H->length = 0;
    H->crnt = (Node *)malloc(sizeof(Node));
    H->head = (Node *)malloc(sizeof(Node));
    H->crnt = NULL;
    H->head = NULL;
    return H;
}

int isEmpty(SinglyCircularLL *list)
{
    return (list->head == NULL);
}

void addLast(SinglyCircularLL *list, element *item)
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

    if (isEmpty(list)) // 헤더 노드와의 연결을 바꾸어주어야 하므로 따로 처리가 필요
    {
        list->head = newNode;
        list->crnt = newNode;
        newNode->rlink = newNode;
    }
    else
    {
        newNode->rlink = list->head; // newNode를 첫 번째 노드에 연결
        list->crnt->rlink = newNode; // 추가되기 전 노드의 오른쪽링크(1번 노드)에 새로운 노드를 연결
        list->crnt = newNode;        // 가리키는 노드를 추가된 노드로 이동
    }
    list->length++;
}
element *delete (SinglyCircularLL *list)
{
    if (isEmpty(list))
    {
        printf("List is EMPTY\n");
        exit(1);
    }
    else
    {
        Node *remove = list->crnt; // 현재 가리키는 노드를 삭제할 노드라고 함.
        element *returnData = &(remove->data);
        if (remove == list->head)
        {
            list->head = remove->rlink;
        }
        Node *prev = list->head;
        while (prev->rlink != remove)
        {
            prev = prev->rlink;
        }
        list->crnt = remove->rlink;
        prev->rlink = remove->rlink;
        list->length--;
        return returnData;
    }
}

element *moveCrnt(SinglyCircularLL *list, int skipNum)
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

int main()
{
    printf("I am Sohn Soo Kyoung\n");
    printf("This Project is No_5 :: Singly Circular Linked List for Escaping Island.\n");
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
    SinglyCircularLL *pplList = NULL;
    pplList = createList();
    isEmpty(pplList);
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
    SinglyCircularLL *loser = createList();

    while (pplList->length > 3)
    {
        element *test = moveCrnt(pplList, skipNum);
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
    Node *finalList = pplList->head;
    printf("배를 타고 무인도를 탈출할 최종 3인은 ");
    for (int i = 0; i < 3; i++)
    {
        if (i == 2)
        {
            printf("%d번 %s 님 입니다. ^^\n", finalList->data.num, finalList->data.name);
        }
        else
        {
            printf("%d번 %s 님, ", finalList->data.num, finalList->data.name);
        }
        finalList = finalList->rlink;
    }
}
```

## 풀이 과정

1. 사람 번호와 이름을 pplList에 넣어줍니다. (addLast() 사용)
2. pplList의 길이가 3이 되기 전까지 moveCrnt()를 통해서 skipNum만큼 crnt를 이동시키면서 해당 노드를 지워줍니다. (moveCrnt(), delete() 사용)
3. 탈락자들만 모은 연결 리스트인 loser를 출력해줍니다. 생존자의 경우 처음 입력받은 연결 리스트에 그대로 있으므로 pplList를 통해서 생존자를 출력해줍니다.
4. 3명의 데이터를 출력해줍니다. <br> <br>

함수 설명 <br>

- SinglyCircularLL \*createList() : 처음 새로운 원형 연결 리스트를 만들 때 사용됩니다. 헤더 노드의 메모리를 할당 받고, 헤더 노드를 구성하고 있는 length는 0으로, crnt, head를 NULL로 초기화 시켜주는 역할을 합니다.
- int isEmpty(SinglyCircularLL \*list) : 리스트가 비어있는 노드인지 아닌지를 판별해줍니다. list->head == NULL 조건이 참이라면 빈 리스트라는 의미로 1을 리턴하고, 그렇지 않다면 0을 리턴합니다.
- void addLast(SinglyCircularLL *list, element *item) : 마지막 노드 뒤에 새로운 노드를 추가해줍니다. 그때의 노드는 item 데이터를 가지고 있습니다.
- element * delete(SinglyCircularLL *list) : list에서 list->crnt를 지워주는 함수입니다.
- element *moveCrnt(SinglyCircularLL *list, int skipNum) : pplList->crnt를 skipNum만큼 이동시켜주는 함수입니다. <br> <br>

변수 설명 <br>

- element 구조체 : 숫자와 사람 이름을 넣기 위해서 만들었습니다 element는 노드의 data부분에 해당합니다.
- Node 구조체 : 하나의 노드이며 노드 안에는 data와 rllink를 구성하고 있습니다.
- SSinglyCircularLL 구조체 : pplList의 시작 부분을 의미하고, 헤더 노드를 가지고 있습니다. 헤더 노드에는 length, crnt, head가 있습니다. length는 리스트의 길이를 가지고 있습니다. crnt는 current의 약자로 현재 가리키고 있는 노드를 뜻합니다. 추가될 때마다 crnt는 한 칸씩 뒤로 이동하며, 지울 노드를 가리키는 데에 사용됩니다. head는 가장 첫 번째 노드를 가리키며, 출력시 오름차순으로 출력될 수 있도록 합니다.
- pplList : 사람의 데이터를 가지고 있는 단순 원형 연결 리스트의 시작 부분입니다.
- skipNum : 규칙에 따라 탈출하지 못할 사람을 고르기 위한 숫자입니다. #include <time.h>에서 srand(time(NULL))을 사용해서 완벽한 랜덤 함수를 출력할 수 있도록 하였습니다. rand()의 경우는 특정 규칙이 있어 랜덤처럼 보이지만 사실 규칙이 정해져있으므로 srand()를 사용하였습니다.
