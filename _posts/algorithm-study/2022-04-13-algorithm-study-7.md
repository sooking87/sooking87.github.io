---
title: "[C] �ܼ� ���� ����Ʈ"
excerpt: "�ܼ� ���� ����Ʈ"
categories: [Algorithm Study]
tags: [Algorithm Study, C, Algorithm]
toc: true
toc_sticky: true
published: true
---

## ? ��� �� �󸮽�Ʈ �����

### ? ��� �����

```c
typedef struct listNode {
    int data;
    struct listNode* link;
} listNode;

typedef struct {
    listNode* head;
} linkedList_h;
```
- listNode : ���
- linkedList_h : ��� ���

### ? �󸮽�Ʈ �����

```c
// ����Ʈ ��ü�� ����Ű�� ���� L ��� �ȿ� head ��� �ֱ�
// ���� ����Ʈ �����
linkedList_h *createLinkedList_h(void) {
    linkedList_h* L;
    L = (linkedList_h*)malloc(sizeof(linkedList_h));
    L->head = NULL;
    return L;
}
```
- ���� ����Ʈ �̸��� ***linkedList_h*** �̴�. 

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
    // p�� ������ ���
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
        //���� ��� : L->head
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

�� �Լ��� ����Ʈ�� �� ����Ʈ�� �� ������ ��带 �޸� ���������ش�. 
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
    return p; //x���� ���� ��尡 ���� ��� NULL�� ��ȯ
}
```

### ? void printList(linkedList_h*)

```c
void printList(linkedList_h *L) {
    listNode* p = L->head;
    if (p == NULL) {
        printf("����� ��尡 �����ϴ�.");
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

