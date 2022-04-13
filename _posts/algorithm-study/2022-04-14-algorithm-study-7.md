---
title: "[C] 단순 연결 리스트"
excerpt: "단순 연결 리스트"
categories: [Algorithm Study]
tags: [Algorithm Study, C, Algorithm]
toc: true
toc_sticky: true
published: true
---

## ? 노드 및 빈리스트 만들기

### ? 노드 만들기

```c
typedef struct listNode {
    int data;
    struct listNode* link;
} listNode;

typedef struct {
    listNode* head;
} linkedList_h;
```
- listNode : 노드
- linkedList_h : 헤더 노드

### ? 빈리스트 만들기

```c
// 리스트 전체를 가리키는 변수 L 노드 안에 head 노드 넣기
// 공백 리스트 만들기
linkedList_h *createLinkedList_h(void) {
    linkedList_h* L;
    L = (linkedList_h*)malloc(sizeof(linkedList_h));
    L->head = NULL;
    return L;
}
```
- 이제 리스트 이름은 ***linkedList_h*** 이다. 

### ? void addLastNode(linkedList_h*, int)

```c
void addLastNode(linkedList_h* L, int x) {
    listNode* newNode;
    listNode* p;
    newNode = (listNode*)malloc(sizeof(listNode));
    newNode->data = x;
    newNode->link = NULL;
    if (L->head == NULL) {
        L->head = newNode;
        return;
    }
    p = L->head;
    while(p->link != NULL) {
        p = p->link;
    }
    // p는 마지막 노드
    p->link = newNode;
}
```

### ? void reverse(linkedList_h*)

```c
void reverse(linkedList_h* L) {
    listNode* lead;
    listNode* middle;
    listNode* tail;

    lead = L->head;
    middle = NULL;
    tail = NULL;
    while (lead != NULL) {
        tail = middle;
        middle = lead;
        lead = lead->link;
        middle->link = tail;
    }
}
```

### ? void deleteLastNode(linkedList_h*)

```c
void deleteLastNode(linkedList_h* L) {
    listNode* crnt;
    listNode* prev;
    if (L->head == NULL) return;
    if(L->head->link == NULL) {
        //선행 노드 : L->head
        free(L->head);
        L->head = NULL;
        return;
    }
    else {
        prev = L->head;
        crnt = L->head->link;
        while(crnt->link != NULL) {
            prev = crnt;
            crnt = crnt->link;
        }
        free(crnt);
        prev->link = NULL;
    }
}
```

### ? void freeLinkedList_h(linkedList_h*)

이 함수는 리스트가 빈 리스트가 될 때까지 노드를 메모리 해제시켜준다. 
```c
void freeLinkedList_h(linkedList_h* L) {
    listNode* p;
    while(L->head != NULL) {
        p = L->head;
        L->head = L->head->link;
        free(p);
        p = NULL;
    }
}
```

### ? listNode \*searchNode(linkedList_h\*, int)

```c
listNode *searchNode(linkedList_h *L, int x) {
    listNode* p;
    p = L->head;
    while (p != NULL) {
        if (p->data == x) {
            return p;
        }
        p = p->link;
    }
    return p; //x값을 가진 노드가 없는 경우 NULL을 반환
}
```

### ? void printList(linkedList_h*)

```c
void printList(linkedList_h *L) {
    listNode* p = L->head;
    if (p == NULL) {
        printf("출력할 노드가 없습니다.");
    }
    else {
        while(p != NULL) {
            printf("%d", p->data);
            p = p->link;

            if (p != NULL) {
                printf(", ");
            }
        }
        printf("\n");
    }
}
```

## ? main()

```c
int main() {
    linkedList_h* L;
    L = createLinkedList_h();
    addLastNode(L, 1);
    addLastNode(L, 2);
    addLastNode(L, 3);
    printList(L);
    addLastNode(L, 4);
    printList(L);
    deleteLastNode(L);
    printList(L);
    deleteLastNode(L);
    printList(L);
    reverse(L);
    printList(L);

    freeLinkedList_h(L);
    printList(L);

    return 0;

}

>>>
1, 2, 3
1, 2, 3, 4
1, 2, 3
1, 2
1
```

