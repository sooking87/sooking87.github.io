---
title: "[데이터 구조 2번] Selection Sort using Bi-directional Circular Linked List"
excerpt: "[데이터 구조 2번] Selection Sort using Bi-directional Circular Linked List"
categories: [Algorithm C_C++]
tags: [Algorithm Study, C/C++, Algorithm]
toc: true
toc_sticky: true
---

## 문제

12개의 입력값을 이중 원형 연결리스트를 사용하여 선택정렬하기

## 풀이

```c++
#include <stdio.h>
#include <stdlib.h>
#define _CRT_SECURE_NO_WARNINGS
#define LENGTH 12

typedef struct Node
{
    int data;
    struct Node *llink;
    struct Node *rlink;
} Node;

typedef struct H
{
    int length;
    Node *crnt;
    Node *head;
} BiDirectionCLL;

BiDirectionCLL *createList()
{
    BiDirectionCLL *H;
    H = (BiDirectionCLL *)malloc(sizeof(BiDirectionCLL));
    H->length = 0;
    H->crnt = (Node *)malloc(sizeof(Node));
    H->head = (Node *)malloc(sizeof(Node));
    H->crnt = NULL;
    H->head = NULL;
    return H;
}

int isEmpty(BiDirectionCLL *bcList)
{
    return (bcList->head == NULL);
}

void addLast(BiDirectionCLL *bcList, int data)
{
    Node *newNode = (Node *)malloc(sizeof(Node));
    if (newNode == NULL)
    {
        fprintf(stderr, "메모리 할당 에러\n");
        exit(1);
    }

    newNode->data = data;

    if (isEmpty(bcList))
    {
        bcList->head = newNode;
        bcList->crnt = newNode;
        newNode->rlink = newNode;
        newNode->llink = newNode;
    }
    else
    {
        newNode->llink = bcList->crnt;
        newNode->rlink = bcList->head;
        bcList->crnt->rlink = newNode;
        bcList->head->llink = newNode;
        bcList->crnt = newNode;
    }
    bcList->length++;
}

void swap(int *standard, int *min)
{
    int temp = *standard;
    *standard = *min;
    *min = temp;
}

void SelectionSort(BiDirectionCLL *bcList)
{
    // 첫 번째 노드부터 시작
    Node *standard = bcList->head; // crnt과 그 이후의 노드를 비교하면서 최소값을 찾을 것
    while (standard->rlink != bcList->head)
    {
        Node *stTemp = standard;
        Node *compare = standard->rlink; // 최소값을 구하기 위한 변수
        int isChanged = 1;
        while (compare != bcList->head)
        {
            if (stTemp->data > compare->data)
            {
                isChanged = 0;
                stTemp = compare;
            }
            compare = compare->rlink;
        }
        if (isChanged == 0)
        {
            swap(&(standard->data), &(stTemp->data));
            Node *afterChanged = bcList->head;
            for (int i = 0; i < LENGTH; i++)
            {
                printf("%d 번째 노드 값: %d\n", (i + 1), afterChanged->data);
                afterChanged = afterChanged->rlink;
            }
            printf("\n");
        }
        standard = standard->rlink;
    }
}
int main()
{
    printf("I am Sohn Soo Kyoung\n");
    printf("This Project is No_2 :: Selection Sort using Bi-directional Circular Linked List.\n");
    printf("Please Cheer Up ! Until 2022.05.23\n\n");

    BiDirectionCLL *bcList = NULL;
    bcList = createList(); // 헤더 노드 만들기

    int data;
    for (int i = 0; i < LENGTH; i++)
    {
        printf("값을 입력해주세요: ");
        scanf("%d", &data);
        addLast(bcList, data);
        // 노드를 입력할 때마다 현재의 bcList의 좌측 및 우측 노드의 값을 프린트하기
        printf("추가된 노드의 좌측 값: %d\n", bcList->crnt->llink->data);
        printf("추가된 노드의 값: %d\n", bcList->crnt->data);
        printf("추가된 노드의 우측 값: %d\n\n", bcList->crnt->rlink->data);
    }

    bcList->crnt = bcList->crnt->rlink;
    SelectionSort(bcList);
    printf("정렬 이후\n오름차순 ver.\n");
    Node *p = bcList->head;
    int cnt = 1;
    int sum = 0;
    double avg;
    while (p->rlink != bcList->head)
    {
        printf("%d 번째 노드: %d\n", cnt, p->data);
        sum += p->data;
        p = p->rlink;
        cnt++;
    }
    printf("%d 번째 노드: %d\n", cnt, p->data);
    sum += p->data;
    avg = sum / (double)LENGTH;
    printf("bcList 내의 %d개의 원소 값의 합: %d\n", LENGTH, sum);
    printf("bcList 내의 %d개의 원소 값의 평균: %f\n", LENGTH, avg);

    printf("\n정렬 이후\n내림차순 ver.\n");
    Node *p2 = bcList->head->llink;
    int cnt2 = 1;
    int sum2 = 0;
    double avg2;
    while (p2->llink != bcList->head->llink)
    {
        printf("%d 번째 노드: %d\n", cnt2, p2->data);
        sum2 += p2->data;
        p2 = p2->llink;
        cnt2++;
    }
    printf("%d 번째 노드: %d\n", cnt2, p2->data);
    sum2 += p2->data;
    avg2 = sum2 / (double)LENGTH;
    printf("bcList 내의 %d개의 원소 값의 합: %d\n", LENGTH, sum2);
    printf("bcList 내의 %d개의 원소 값의 평균: %f\n", LENGTH, avg2);
}
```

## 풀이 과정

1. 먼저 scanf 함수를 통해서 12개의 값을 입력받습니다. 입력을 받을 때마다 추가된 데이터를 기준으로 앞쪽 노드, 뒤쪽 노드의 데이터를 출력해줍니다.
2. 선택 정렬을 진행합니다. 이때 SelectionSort() 와 swap()이 사용됩니다.
3. SelectionSort()를 마치고 나서 첫 번째 노드 기준 양방향으로 출력하여 오름 차순으로 정렬됨을 확인하고, 마지막 노드를 기준으로 역방향으로 출력하여 내림 차순으로 정렬됨을 확인합니다. <br>
   <br>

- Node 구조체 : 노드를 구성하고 있으며 구조체는 data, llink, rlink로 구성되어 있어 이중 연결 리스트를 만들기 위한 노드를 만들었습니다
- BiDirectionCLL 구조체 : 헤더 노드를 위한 값들이 들어가 있으며 연결 리스트의 길이를 나타내는 length와 현재 가리키는 노드를 나타내는 crnt, 첫 노드를 가리키는 head로 구성되어 있습니다. 따라서 H->length는 연결 리스트의 길이로 사용하였고, H->crnt는 현재 가리키는 노드, H->head는 첫 번째 노드를 가리킵니다.
- bcList : 문제에서 요구하는 이중 원형 연결 리스트의 시작 부분입니다.
- BiDirectionCLL \*createList() : 헤더 노드도 없는 bcList에 헤더 노드를 만들어주고 bcList가 가리키는 노드는 헤더 노드로 하고, 길이를 0으로 초기화하고, head와 crnt가 가리키는 노드는 없으로 NULL로 해줍니다.
- int isEmpty(BiDirectionCCL \*bcList) : 빈 리스트인지 아닌지를 판별합니다. 1이면 빈 리스트이고 0이면 비어 있지 않은 리스트입니다.
- void addLast(BiDirectionCCL \*bcList) : 입력 받은 data를 제일 마지막 노드로 연결시켜주는 함수입니다. 첫 노드라면 bcList->head와 bcList->crnt를 모두 첫 노드에 연결시키고, 원형 이중 연결 리스트를 위해서 newNode의 llink와 rlink를 newNode로 연결시킵니다. <br>
  첫 노드가 아니라면 newNode->llink를 추가할 노드 앞쪽노드(bcList->crnt)에 연결시키고 newNode->rlink를 첫 노드(bcList->head)와 연결시킵니다. 그리고 newNode의 앞쪽 노드의 rlink를 newNode에 연결시키고, 첫 노드의 llink를 newNode에 연결시켜서 원형 이중 연결 리스트의 구조를 만들어줍니다.
- void swap(int *standard, int *min) : 값을 바꾸어주는 함수입니다.
- void SelectionSort(BiDirectionCLL \*bcList) : 선택 정렬이 이루어지는 함수입니다.
