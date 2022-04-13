---
title: "[JAVA] 연결 리스트"
excerpt: "선형 리스트, 연결 리스트"
categories: [Algorithm Study]
tags: [Algorithm Study, Java, Algorithm]
toc: true
toc_sticky: true
---

## ✨선형 리스트

### 📖 선형 리스트란?

리스트는 데이터를 **순서대로** 나열해 놓은 자료구조를 말한다. 가장 단순한 구조를 이루고 있는 리스트를 선형 리스트 또는 연결 리스트라고 한다. 하지만 선형 리스트의 경우 추가된 노드를 중간에 추가하기 위해서는 삽입 요소 다음의 요소를 하나씩 밀어야 되고, 삭제하는 경우에도 삭제 요소 뒤에 요소들을 모두 앞으로 당겨야 한다. 그렇기 때문에 선형 리스트는 다음과 갖게 된다.

- 쌓이는 데이터의 크기를 미리 알아야 한다.
- 데이터의 삽입, 삭제에 따라 남은 데이터를 모두 옮겨야 하기 때문에 효율이 좋지 않다.

## ✨연결 리스트

### 📖 포인터로 연결 리스트 만들기

노드 형이 클래스 Node<E> 형인 연결 리스트를 클래스 L:inkedList<E>로 구현한 프로그램이다.

💡

```java
package LIST;

public class LinkedList<E> {
    class Node<E> {
        private E data; //데이터
        private Node<E> next; //뒤쪽 포인터

        //클래스 Node<E>의 생성자
        Node(E date, Node<E> next) {
            this.data = data;
            this.next = next;
        }
    }

    private Node<E> head; //머리노드
    private Node<E> crnt; //temp와 같은 존재

    //클래스 LinkedList()의 생성자
    public LinkedList() {
        head =  crnt = null;
    }
}
```

- data : 데이터를 가리키는 주소
- next : 다음 노드를 가리키는 포인터
- 클래스 Node<E>의 생성자 : 현재 인수로 전달받은 data와 next를 인자로 설정
- Node<E> head : 머리 노드
- Node<E> crnt : 현재 노드
- 클래스 LinkedList()의 생성자 : head와 crnt를 null로 초기화
  <br><br>
- 노드 0개 : 🎧(head) -> null
  - 연결리스트가 비어있는지 판단하는 방법
    ```java
    head == null;
    ```
- 노드 1개 : 🎧 -> data | null
  - 노드가 1개인 연결 리스트 판단하는 방법
    ```java
    head.next == null;
    ```
- 노드 2개 : 🎧 -> data | refer -> data | null -노드가 2개인 연결 리스트 판단하는 방법
  ```java
  head.next.next == null;
  ```
- 꼬리 노드인지 판단하는 방법

  Node<E>형 변수인 p가 리스트의 노드중 하나를 가리킬 때, _p.next == null;_ 이라면 꼬리노드 이다.

#### 📍 search 메소드

노드 스캔은 아래의 조건 중 하나만 성립하면 종료된다.

1. 검색 조건을 만족하는 노드를 찾지 못하고 꼬리 노드로 도달했을 경우
2. 검색 조건을 만족하는 노드를 찾은 경우

💡

```java
// 노드 검색
public E search(E obj, Comparator<? super E> c) {
    Node<E> ptr = head;                      //현재 스캔 중인 노드

    while (ptr != null) {
        if (c.compare(obj, ptr.data) == 0) { //검색 성공
            crnt = ptr;
            return ptr.data;
        }
        ptr = ptr.next;                     //다음 노드와 검색 시도
    }
    return null;                            //검색 실패
}
```

- 제네릭 데이터형 E를 반환하는 메소드 search()
- obj : 검색할 key
- c : 선택한 노드와 key값을 비교

처음에 🎧로 시작해서 노드의 데이터와 key값을 비교하면서 다른 값이라면 다음 노드를 검색하고 같은 값이라면 crnt에 ptr을 대입하고, ptr.data를 리턴한다.(검색 메소드 종료조건 2) 그리고 while문이 종료된다면 검색하는 데이터가 없다는 뜻이므로 null을 리턴한다.(검색 메소드 종료조건 1)

#### 📍 addFirst 메소드

📌add 메소드는 꼭 주의해야되는 순서가 있다. <br>
1. newNode의 데이터필드 삽입
2. newNode의 다음 노드 링크를 링크 필드에 연결
3. 추가했을 때, 그 전 노드의 링크 필드를 추가 노드에 연결

```java
// addFirst 메소드
public void addFirst(E obj) {
    Node<E> ptr = head; //추가 노드의 다음 노드를 🎧로 바꾼다. 즉, 머리 노드에 대한 포인터를 ptr에 저장
    head = crnt = new Node<E>(obj, ptr); //머리 노드를 obj가 포함된 포인터로 바꾸고 머리 노드의 다음 포인터를 ptr로 바꾼다.
}
```

결국 연결 리스트들은 p.next의 주소에 따라서 연결이 되어있기 때문에 만약에 A -> B -> C라는 리스트 맨 앞에 D를 추가하고 싶다면 노드 A에 대한 포인터를 D의 포인터 자리에 넣어주면 된다.

- sol

1. 삽입 전의 머리 노드 A에 대한 포인터를 ptr에 대입한다.
2. 삽입할 노드 D를 _new Node<E>(obj, ptr)_ 를 통해서 생성한다. <br>
   그리고 생성한 노드를 참조하도록 head를 업데이트한다. <br>
   ❓ -> 그러면 A의 참조값은 뭘로 추가해 준거지? 🅰️ : ptr

#### 📍 addLast 메소드

```java
//addLast 메소드
public void addLast(E obj) {
    if (head == null) {                            //연결 리스트에 노드가 없다면
        addFirst(obj);                             //addFirst 메소드와 같음
    }
    else {
        Node<E> ptr = head;                        //현재 검색 중인 노드
        while (ptr.next != null) {
            ptr = ptr.next;                        //while문이 종료될 때, ptr은 꼬리 노드를 가리킨다.
        }
        ptr.next = crnt = new Node<E> (obj, null); //(전)꼬리 노드.next에 (현)꼬리 노드 객체를 생성해준다.
    }
}
```

addFirst 메소드와 원리는 비슷하다. addFirst 메소드 같은 경우는 굳이 마지막의 노드를 찾을 필요 없이 그냥 첫 번째 노드의 참조값을 뽑아서 추가할 값의 다음 주소값으로 넣어주면 된다. 하지만 addLast의 값은 마지막 노드를 찾아야 되므로 else문을 수행하면서 마지막 노드 다음에 Node<E> 생성자를 추가해준다.

#### 📍 removeFirst 메소드

📌remove 메소드는 꼭 주의해야되는 순서가 있다. <br>
1. Node를 삭제하고 싶어 -> 얘를 removeNode라고 하자
2. removeNode의 선행 노드 찾기
3. removeNode의 전 노드와 다음 노드를 연결 <br>

removeFirst 메소드의 경우에는 노드가 0개일때를 제외하고 실행해야 된다.

💡

```java
// removeFirst 메소드
public void removeFirst() {
    if (head != null) {
        head = crnt = head.next; //head는 머리 노드를 가리키는데, 가리키는 것을 머리 노드 다음 노드로 바꿈
    }
}
```

추가든 제거든 첫 번째 노드를 건드리는 메소드는 전반적으로 간단한 편이다. 굳이 마지막 노드를 구할 필요 없이 노드가 최소 1개라면 첫 번째 노드가 있는 것이기 때문이다. 첫 번째 노드를 지우는 방법은 **head에 대한 참조를 2번째 노드로 설정해두면 된다.** (So Simple🛩️)

#### 📍 removeLast 메소드

```java
// removeLast 메소드
public void removeLast() {
    if (head != null) {
        if (head.next == null) {           //노드가 1개라면
            removeFirst();
        } else {
            Node<E> ptr = head;            // 현재 검색 중인 노드
            Node<E> pre = head;            // ptr 앞쪽 노드

            while (ptr.next != null) {
                pre = ptr;
                ptr = ptr.next;
            }
            pre.next = null;
            crnt = pre;                   //ptr을 해체한다.
        }
    }
}
```

마지막 노드를 제거하는 방법은 노드가 1개라면 _removeFirst()_ 와 같으므로 따로 처리해주었고, 노드가 2개 이상이라면, **ptr** 변수와 **pre** 변수를 만들었다. ptr은 현재의 노드를 말하고, pre는 ptr의 앞의 노드를 말한다. _removeLast()_ 에서 pre를 굳이 사용 해주는 이유는 ptr.next의 값이 null인 경우 앞의 노드까지 사용할 것이기 때문이다.

#### 📍 remove 메소드

remove 메소드는 임의의 노드를 삭제하는 메소드이다.

```java
// remove 메소드
// 노드 p를 삭제
public void remove(Node p) {
    if (head == null) {
        removeFirst();
    } else {
        Node<E> ptr = head;
        while (ptr.next != p) {   //현재 p를 삭제하고자 하는데, p와 ptr이 다르다면
            ptr = ptr.next;       //다음 노드와 검사
            if (ptr == null)      //근데 ptr == null이라는 말은 꼬리 노드 였다는 말
                return;           //p가 리스트에 없습니다.
        }
        ptr.next = p.next;        //원래 ptr.next = p인데, 그 p를 없애기 위해서 ptr.next = p.next로 만들어 머림.
        crnt = ptr;               //p를 해체한다.
    }
}

// 선택 노드를 삭제
public void removeCurrentNode() {
    remove(crnt);
}
```

#### 📍 clear() 메소드

```java
// 모든 노드 선택
public void clear() {
    while (head != null) {
        removeFirst();
    }
    crnt = null; //head.next = null이 되버림
}
```

#### 📍 next() 메소드

```java
// 선택 노드를 하나 뒤쪽으로 이동
public boolean next() {
    if (crnt == null || crnt.next == null) {
        return false;
    }
    crnt = crnt.next;
    return true;
}
```

#### 📍 printCurrentNode() 메소드

```java
// 선택 노드를 출력
public void printCurrentNode() {
    if (crnt == null) {
        System.out.println("선택한 노드가 없습니다.");
    } else {
        System.out.println(crnt.data);
    }
}
```

#### 📍 dump() 메소드

```java
// 모든 노드를 출력
public void dump() {
    Node<E> ptr = head;
    while (ptr != null) {
        System.out.println(ptr.data);
        ptr = ptr.next;
    }
}
```

### 📖 커서로 연결 리스트 만들기

여기서 커서란 앞에서 다음 노드의 포인터 역할을 대신한다. 앞 장에서 본 연결 리스트 같은 경우는 노드용 객체를 위한 메모리 영역을 만들고 해체하는 작업이 필요했다.(_Node<E> ptr = head;_) 하지만 커서로 연결 리스트를 만들게 된다면 커서를 통해 다음에 올 인덱스를 알 수 있기 때문에 노드용 객체를 만들 필요가 없다. **여기서 전제는 데이터 수의 최댓값을 미리 알 수 있다고 가정할 때이다.**

💡

```java
package LIST;

import java.util.Comparator;

public class AryLinkedList<E> {

    // 노드
    class Node<E> {
        private E data;
        private int next; // 리스트의 뒤쪽 포인터
        private int dnext; // free 리스트의 뒤쪽 포인터

        // data와 next를 설정
        void set(E data, int next) {
            this.data = data;
            this.next = next;
        }
    }

    private Node<E>[] n; // 리스트 본체
    private int size; // 리스트의 용량(가장 큰 데이터 수)
    private int max; // 사용 중인 꼬리 record
    private int head; // 머리노드
    private int crnt; // 선택 노드
    private int deleted; // free 리스트의 머리 노드
    private static final int NULL = -1; // 다음 노드 없음 / 리스트 가득 참

    // 생성자
    public AryLinkedList(int capacity) {
        head = crnt = max = deleted = NULL;
        try {
            n = new Node[capacity];
            for (int i = 0; i < capacity; i++) {
                n[i] = new Node<E>();
            }
            size = capacity;
        } catch (OutOfMemoryError e) { //배열 생성 실패
            size = 0;
        }
    }
```

- free 리스트 : 사용하지 않는 빈 배열, 즉 삭제한 여러 레코드를 관리하기 위해 사용하는 자료구조
- record : 배열에 있는 노드 != 연결 리스트의 노드
  - ex. 연결 리스트 : A -> B -> C -> D <br>
    배열 : B -> C -> D -> A <br>
    이라고 할 때, A는 연결 리스트에서 머리 노드에 해당하지만 배열의 마지막 인덱스에 존재하기 때문에 A는 연결 리스트에서 **머리 노드**이자 배열에서 **3번째 레코드**가 된다.
- data : 리스트의 값
- next : 다음 data의 인덱스
- dnext : free 리스트의 뒤쪽 포인터
- size : 리스트의 사이즈
- max : 사용 중인 꼬리 record, 즉 배열의 가장 꼬리 쪽에 들어 있는 노드의 레코드 번호
- head : 머리 노드
- crnt : 선택 노드
- deleted : free 리스트의 머리 노드
- n : n이라는 리스트를 선언 -> capacity의 양만큼 노드 리스트를 만듬

#### 📍 getInsertIndex() 메소드

다음에 삽입하는 record의 인덱스를 구한다.

```java
// 다음에 삽입하는 record의 인덱스를 구함
// 추가할 노드의 위치를 알려줌
private int getInsertIndex() {
    if (deleted == NULL) {         //삭제할 record가 없다면
        if (max < size)
            return ++max;          //새로운 record생성
        else {                     //max >= size 라는 것은 리스트 용량이 넘친다는 말
            return NULL;
        }
    }
    else {                         //deleted != NULL라면 프리 리스트에 레코드가 존재한다는 말
        int rec = deleted;         //free 리스트에서
        deleted = n[rec].dnext;
        return rec;
    }
}
```

#### 📍 record idx를 free 리스트에 등록

```java
// 삭제한 레코드를 free 리스트에 등록
// stack처럼 가장 나중에 프리 리스트에 들어온 값이 가장 먼저 연결 리스트로 빠짐
private void deleteIndex(int idx) {
    if (deleted == NULL) {   //프리 리스트에 레코드가 없다면
        deleted = idx;       //매개변수의 인덱스를 프리 리스트이 머리 노드로 만들어
        n[idx].dnext = NULL; //그리고 그 값 다음에는 없기 때문에 다음 포인터는 NULL로 세팅
    } else {                 //프리 리스트에 레코드가 있다면
        int rec = deleted;   //idx를 프리 리스트의
        deleted = idx;       //머리에 삽입
        n[idx].dnext = rec;
    }
}
```

#### 📍 search() 메소드

```java
// 노드를 검색
public E search(E obj, Comparator<? super E> c) {
    int ptr = head;                              //현재 스캔 중인 노드
    while (ptr != NULL) {                        //꼬리 노드가 아니라면
        if (c.compare(obj, n[ptr].data) == 0) {  //obj와 스캔 중인 노드의 값을 비교해서 같은 값이라면
            crnt = ptr;
            return n[ptr].data;                  //검색 성공
        }
        ptr = n[ptr].next;                       //같지 않다면 다음 인덱스로 맞춤
    }
    return null;                                 //검색 실패
}
```

#### 📍 addFirst() 메소드

```java
// 머리에 노드를 삽입
public void addFirst(E obj) {
    int ptr = head;             //현재 스캔 중인 노드
    int rec = getInsertIndex(); //삽입 전의 머리 노드
    if (rec != NULL) {          //연결 리스트에 값이 있다면
        head = crnt = rec;      //인덱스 rec인 record에 삽입
        n[head].set(obj, ptr);
    }
}
```

- getInsertIndex() 메소드를 통해서 추가될 값이 어디에 위치해야되는지 배열 n중에서 머리 노드의 인덱스를 반환해주는 메소드이다.

#### 📍 addLast() 메소드

```java
// 꼬리에 노드를 삽입
public void addLast(E obj) {
    if (head == NULL) {                   //연결 리스트에 머리 노드가 NULL이라면 = 노드가 없다는 말이므로
        addFirst(obj);                    //머리에 노드 삽입과 같은 말
    } else {
        int ptr = head;                   //현재 스캔 중인 노드
        while (n[ptr].next != NULL) {     //다음 노드의 포인터가 NULL이기 전까지 while문 돌려
            ptr = n[ptr].next;            //ptr은 ptr의 다음 인덱스를 가진 변수
            int rec = getInsertIndex();
            if (rec != NULL) {            //n의 용량이 넘치지 않는다면
                n[ptr].next = crnt = rec;
                n[rec].set(obj, NULL);
            }
        }
    }
}
```

- getInsertIndex() 메소드를 통해서 추가될 값이 어디에 위치해야되는지 배열 n중에서 머리 노드의 인덱스를 반환해주는 메소드이다.

#### 📍 removeFirst() 메소드

```java
// 머리 노드를 삭제
public void removeFirst() {
    if (head != NULL) {
        int ptr = n[head].next;
        deleteIndex(head);
        head = crnt = ptr;
    }
}
```

- deleteIndex(int idx) 메소드 같은 경우, 연결 리스트에서 삭제된 인덱스를 프리 리스트의 머리 노드(deleted)로 옮겨 준다.

#### 📍 removeLast() 메소드

```java
// 꼬리 노드를 삭제
public void removeLast() {
    if (head != NULL) {
        if (n[head].next == NULL) {
            removeFirst();
        } else {
            int ptr = head;
            int pre = head;

            while (n[ptr].next != NULL) {
                pre = ptr;
                ptr = n[ptr].next;
            }
            n[pre].next = NULL;
            deleteIndex(ptr);
            crnt = pre;
        }
    }
}
```

- deleteIndex(int idx) 메소드 같은 경우, 연결 리스트에서 삭제된 인덱스를 프리 리스트의 머리 노드(deleted)로 옮겨 준다.

#### 📍 그 외의 나머지 메소드는 포인터 연결 리스트와 유사

### 🌟 커서를 이용한 연결 리스트의 포인트

포인터를 이용한 연결 리스트의 단점은 삽입, 삭제를 수행할 때마다 노드용 객체를 위한 메모리 영역을 만들고 해체하는 과정이 필요였다.

- 해결책 : 배열 n에 연결 리스트와 프리 리스트를 만들자!
- 프리 리스트는 연결 리스트에서 삭제된 노드의 인덱스를 가져와서 다음 연결 리스트에 값이 추가될 때 어디에 추가해야되는지를 알려준다.( **getInsertIndex** )
- 연결 리스트에서 값이 삭제된다면 프리 리스트에 해당 인덱스를 추가한다. ( **deleteIndex** )
