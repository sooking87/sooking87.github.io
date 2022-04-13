---
title: "[JAVA] 원형 리스트, 원형 이중 연결 리스트"
excerpt: "원형 리스트, 원형 이중 연결 리스트"
categories: [Algorithm Study]
tags: [Algorithm Study, Java, Algorithm]
toc: true
toc_sticky: true
---

## ✨원형 리스트

### 📖 원형 이중 연결 리스트

#### 📍 원형 리스트

원형 리스트는 연결 리스트에서 꼬리 노드가 머리 노드를 가리키는 것이다. 즉 연결 리스트에서는 꼬리 노드의 포인터가 _null_ 이었다면, 원형 리스트에서 꼬리 노드의 포인터는 머리 노드이다.

- ListNode 클래스

  ```java
    class ListNode {
    String data;
    ListNode next;

    public ListNode() {
        this.data = null;
        this.next = null;
    }

    public ListNode(String data) {
        this.data = data;
        this.next = null;
    }

    public ListNode(String data, ListNode next) {
        this.data = data;
        this.next = next;
        this.next = null;
    }

    public String getData() {
        return this.data;
    }
  }
  ```

- LinkedList`<`E`>` 클래스

  ```java
  public class copyCircleLinkeList {
  private ListNode head;

  public copyCircleLinkeList() {
      this.head = null;
  }

  //...메서드 추가
  ```

#### 📍 원형 리스트의 특징

원형 리스트의 경우, 꼬리 노드가 결국 머리 노드를 가리키고 있기 때문에 마지막 노드를 삽입하는 것이 곧 리스트의 첫 번째에 노드를 삽입하는 것과 같습니다.

#### 📍 addLast() 메소드

```java
// 꼬리 노드에 삽입
  public void addLast(String str) {
      ListNode node = new ListNode(str);
      if (head == null) {
          head = node; // 리스트 새로운 노드를 추가
          node.next = node; // 새 노드의 다음 노드가 자기 자신을 가리키게 하여 원형 연결 리스트를 만듬
      } else {
          ListNode current = head; // 첫 번째 노드에 대한 참조값을 current변수에 넣는다.
          while (current.next != head) { // 꼬리 노드까지 이동
              current = current.next;
          }
          // current = 꼬리 노드
          node.next = current.next; // current.next는 헤드 노드이므로 꼬리 노드의 다음 노드를 헤드로 연결
          current.next = node;
      }
  }
```

#### 📍 addFirst() 메소드

```java
// 첫번째 노드에 삽입
public void insertFirstNode(String str) {
    ListNode node = new ListNode(str);
    if (head == null) {
        head = node;
    } else {
        ListNode current = head;
        while (current.next != head) {
            current = current.next;
        }
        node.next = current.next;
        current.next = node;
        head = node;
    }
}
```

_addLast()_ 와 거의 동일하고 마지막에 헤드 부분의 연결 노드만 바뀌는 것을 알 수 있다. 즉, 원형 리스트는 내가 몇 번째 노드를 제일 마지막으로 보느냐의 차이이고, 추가할 때는 마지막 노드에 추가하는 것처럼 해도 된다.

#### 📍 add() 메소드

```java
// 노드 삽입
public void add(ListNode pre, String str) {
    ListNode node = new ListNode(str);
    if (head == null) {
        head = node;
    } else {
        ListNode current = head;
        while (current.next != pre) {
            current = current.next;
        }

        current = current.next; // current.next는 pre노드와 같았는데, 이 코드를 통해서 결국, current는 pre노드가 됨.
        node.next = current.next;
        current.next = node; //
    }
}
```

#### 📍 removeLast() 메소드

```java
// 마지막 노드 삭제
  public void removeLast() {
      if (head == null) {
          System.out.println("삭제할 노드가 없습니다.");
      } else {
          ListNode prev = head;
          ListNode current = head.next;
          while (current.next != head) {
              prev = current;
              current = current.next;
          }
          prev.next = current.next;
      }
  }
```

#### 📍 removeFirst() 메소드

```java
// 첫 번째 노드 삭제
  public void removeFirst() {
      if (head == null) {
          System.out.println("삭제할 노드가 없습니다.");
      } else {
          ListNode current = head;
          while (current.next != head) {
              current = current.next;
          }
          ListNode old = current.next;
          head = old.next;
          current.next = head;
      }
  }
```

#### 📍 remove() 메소드

```java
// 중간 노드를 삭제
public void remove(String str) {
    ListNode node = new ListNode(str);
    if (head == null) {
        System.out.println("삭제할 노드가 없습니다.");
    } else {
        ListNode prev = head;
        ListNode current = head.next;
        while (current.data != node.data) {
            prev = current;
            current = current.next;
        }
        prev.next = current.next;
    }
}
```

### 📖 이중 연결 리스트

연결 리스트의 큰 단점은 다음 노드를 찾기는 쉽지만, 앞쪽의 노드를 찾을 수 없다는 점이다. 그래서 이 단점을 개선한 자료구조가 이중 연결 리스트이다. 그렇기 때문에 이중 연결 리스트는 3개의 필드가 있는 클래스 Node<E>를 사용한다.

```java
class Node<E> {
    E data;
    Node<E> prev;
    Node<E> next;
}
```

### 📖 원형 이중 연결 리스트

- Node<E> 클래스

  ```java
  //노드
  class Node<E> {
      private E data;
      private Node<E> prev;
      private Node<E> next;

      //Node<E> 생성자
      Node() {
          data = null;
          prev = next = this;
      }

      //Node<E> 생성자
      Node(E obj, Node<E> prev, Node<E> next) {
          data = obj;
          this.prev = prev;
          this.next = next;
      }
  }
  ```

  1. Node()
     자기 자신의 노드가 앞쪽 노드이면서 동시에 다음 노드가 된다.
  2. Node(E obj, Node<E> prev, Node<E> next)
     데이터 obj 앞쪽 포인터가 prev이고 뒤쪽 포인터가 next이다.

- DbLinkedList<E> 클래스

  ```java
  public class DbLinkedList<E> {
  //노드

  /*
  Node<E> 클래스
  */

  private Node<E> head;
  private Node<E> crnt;

  //DbLinkedList<E>의 생성자
  public DbLinkedList() {
      head = crnt = new Node<E>(); //더미 노드 생성
  }
  ```

  1. head : 머리 노드
  2. crnt : 선택 노드
  3. 생성자 : head와 crnt가 가리키는 곳은 더미노드로, 자기 자신을 가리키도록 초기화합니다. 더미 노드는 노드의 삽입과 삭제 처리를 원활하게 하도록 도와줍니다.

- isEmpty() 메소드

  ```java
  //리스트가 비어 있는가
  public boolean isEmpty() {
      return head.next == head;
  }
  ```

리스트에 더미 노드만 있는지 없는지를 조사하는 메소드이다. 만약에 리스트에 더미 노드만 있다면 head.next가 가리키는 곳과 head가 가리키는 곳이 같을 것이다. 여기서 더미 노드만 있다면 그 리스트는 빈 리스트라는 것이므로 _true_ 를 반환하고, 빈 리스트가 아니라면 _false_ 를 반환한다.

#### 📍 search 메소드

```java
//노드를 검색
public E search(E obj, Comparator<? super E> c) {
    Node<E> ptr = head.next;                  //현재 스캔 중인 노드

    while (ptr != head) {
        if (c.compare(obj, ptr.data) == 0) {
            crnt = ptr;
            return ptr.data;                 //검색 성공
        }
        ptr = ptr.next;                      //다음 노드로 선택
    }
    return null;                             //검색 실패
}
```

연결 리스트의 search 메소드와 유사하다. 하지만 원형 이중 연결 리스트에는 더미 노드가 있기 때문에 검색을 해야되는 시작 부분은 **head.next** 라는 차이점이 존재한다. 그리고 연결 리스트일때는 **ptr != null** 일때까지 조사를 했지만 원형 이중 연결 리스트의 경우는 포인터가 null인값이 없으므로 **더미 노드를 가리키는 순간**이 처음으로 돌아왔다는 뜻이다.

#### 📍 printCurrentNode() 메소드

```java
// 선택 노드를 출력
public void printCurrentNode() {
    if (isEmpty()) {
        System.out.println("선택 노드가 없습니다.");
    } else {
        System.out.println(crnt.data);
    }
}
```

- 연결 리스트의 경우 if문 조건 : crnt == null
- 원형 이중 연결 리스트의 경우 if문 조건 : isEmpty()

#### 📍 dump() 메소드

```java
// 모든 노드를 출력
public void dump() {
    Node<E> ptr = head.next;

    while (ptr != head) {
        System.out.println(ptr.data);
        ptr = ptr.next;
    }
}
```

- 연결 리스트의 경우
  - 현재 검색 중인 노드 : Node<E> ptr = head;
  - while 문 조건 : ptr != null
- 원형 이중 연결 리스트의 경우
  - 현재 검색 중인 노드 : Node<E> ptr = head.next;
  - while 문 조건 : ptr != head

#### 🌟 dumpReverse() 메소드

```java
// 모든 노드를 거꾸로 출력
public void dumpReverse() {
    Node<E> ptr = head.prev;

    while (ptr != head) {
        System.out.println(ptr.data);
        ptr = ptr.prev;
    }
}
```

연결 리스트의 경우 앞쪽을 참조할 수 있는 포인터는 없었으므로 없을 수 밖에 없던 메소드! 하지만 원형 이중 연결 리스트에서는 앞쪽 노드를 참조할 수 있는 포인터도 있기 때문에 이런 메소드를 만들 수 있다.

#### 📍 next() 메소드

```java
// 선택 노드를 하나 뒤쪽으로 이동
public boolean next() {
    if (isEmpty() || crnt.next == head) {
        return false;
    }
    crnt = crnt.next;
    return true;
}
```

- 연결 리스트의 경우 if문 조건 : crnt == null || crnt.next == null
- 원형 이중 연결 리스트의 경우 if문 조건 : isEmpty() || crnt.next == head

#### 🌟 prev() 메소드

```java
// 선택 노드를 하나 앞쪽으로 이동
public boolean prev() {
    if (isEmpty() || crnt.prev == head) {
        return false;
    }
    crnt = crnt.prev;
    return true;
}
```

이 메소드 역시 마찬가지 앞쪽을 참조하는 경우이므로 연결 리스트에는 없었다가 원형 이중 연결 리스트의 특징을 이용하여 만들 수 있는 메소드.

#### 🌟add() 메소드

```java
// 선택 노드의 바로 뒤에 노드를 삽입
public void add(E obj) {
    Node<E> node = new Node<E>(obj, crnt, crnt.next);
    crnt.next = crnt.next.prev = node;
    crnt = node;
}
```

crnt.next(node가 위치될 곳)을 node로 대입시키고, crnt.next.prev(node의 앞쪽 포인터)가 가리키는 곳을 node로 대입시킴,,

💡 addFirst(E obj) 메소드

```java
// 머리에 노드를 삽입
public void addFirst(E obj) {
    crnt = head;
    add(obj);
}
```

즉 예를 들어서 리스트에<br>

**더미 노드 -> A** 가 있는데 노드 B를 처음에 추가시키고 싶다면 <br>
선택 노드를 head로 바꾸고 _add(추가할 노드)_ 메소드를 호출 <br>
노드 B의 인스턴스를 만들어. 이 노드의 앞쪽 노드는 head이고, 뒤쪽 노드는 노드 A인 상태 <br>
그리고 crnt.next가 가리키는 것은 head 뒤쪽 노드를 가리키며 이게 추가할 노드 B가 됨. 그리고 crnt.next.prev라는 것은 노드 A의 앞쪽 노드가 추가할 노드 B가 되는 것을 알 수 있다. 그리고 현재 선택 노드는 추가된 노드로 바꿔줌.

💡 addLast(E obj) 메소드

```java
// 꼬리에 노드를 삽입
public void addLast(E obj) {
    crnt = head.prev;
    add(obj);
}
```

에를 들어서 리스트에 <br>

**더미 노드 -> A** 가 있는데, 노드 B를 제일 뒤에 추가시키고 싶다면 <br>
선택 노드를 head의 앞쪽 노드 즉, 꼬리 노드로 바꾸고 _add(추가할 노드)_ 메소드를 호출<br>
노드 B의 인스턴스를 만들면, 앞쪽 노드는 (전)꼬리 노드가 되고, 뒤쪽 노드는 더미 노드가 된다. <br>
그리고 crnt.next((전)꼬리 노드의 뒤쪽 노드)가 가리키는 노드를 추가한 노드 B로 만들고, crnt.next.prev(더미 노드의 앞쪽 노드)가 가리키는 노드를 노드 B로 만들어 준다.

#### 🌟 remove() 메소드

💡 removeCurrentNode() 메소드

```java
// 선택 노드를 삭제
public void removeCurrentNode() {
    if (!isEmpty()) {
        crnt.prev.next = crnt.next;
        crnt.next.prev = crnt.prev;
        crnt = crnt.prev;
        if (crnt == head)
            crnt = crnt.next;
    }
}
```

현재 선택 노드의 노드를 삭제하고자 하는 메소드이다. 삭제하고자 하는 노드를 crnt로 두고, crnt의 앞쪽 노드와 뒤쪽 노드를 연결시켜주면 된다.

💡 remove(Node<E> p) 메소드

```java
// 노드 p를 삭제
public void remove(Node<E> p) {
    Node<E> ptr = head.next;

    while (ptr != head) {
        if (ptr == p) {
            crnt = p;
            removeCurrentNode();
            break;
        }
        ptr = ptr.next;
    }
}
```

노드 p를 삭제하고 싶으므로 삭제하고 싶은 노드를 선택 노드로 해주고, _removeCurrentNode()_ 를 호출해준다.

💡 removeFirst() 메소드

```java
// 머리 노드를 삭제
public void removeFirst() {
    crnt = head.next;
    removeCurrentNode();
}
```

마찬가지로 첫 번째 노드를 삭제하고 싶으므로 선택 노드를 머리 노드로 바꾸어 준다.

💡 removeLast() 메소드

```java
// 꼬리 노드를 삭제
public void removeLast() {
    crnt = head.prev;
    removeCurrentNode();
}
```

마찬가지로 첫 번째 노드를 삭제하고 싶으므로 선택 노드를 꼬리 노드로 바꾸어 준다.

```java
// 모든 노드를 삭제
public void clear() {
    if (!isEmpty()) {
        removeFirst();
    }
}
```
