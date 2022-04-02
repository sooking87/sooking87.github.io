---
title: "[JAVA] 스택"
excerpt: "스택"
categories: [Algorithm Study]
tags: [Algorithm Study, Java, Algorithm]
toc: true
toc_sticky: true
published: true
---

## ✨스택

### 📖 스택이란?

데이터를 일시적으로 저장하기 위해 사용하는 자료구조로, 데이터의 입력과 출력 순서는 후입선출이다.

#### 📍 스택 생성자

```java
package STACK;

public class IntStack {
    private int max; // 스택 용량
    private int ptr; // 스택 포인터
    private int[] stk; // 스택 본체

    // 실행 시 예외 : 스택이 비어 있음
    public class EmptyIntStackException extends RuntimeException {
        public EmptyIntStackException() {
        };
    }

    // 실행 시 예외: 스택이 가득 참
    public class OverflowIntStackException extends RuntimeException {
        public OverflowIntStackException() {
        };
    }

    // 생성자
    public IntStack(int capacity) {
        ptr = 0;
        max = capacity;
        try {
            stk = new int[max];
        } catch (OutOfMemoryError e) {
            max = 0;
        }
    }
```

- max: 스택의 용량을 나타내는 필드
- ptr: 스택에 쌓여있는 데이터 수를 나타내는 필드
- stk: 푸시된 데이터를 저장하는 스택 본체의 배열

#### 📍 push 메소드

데이터를 `IntStack` 배열에 넣어주는 메소드이다.

```java
public int push(int x) throws OverflowIntStackException {
    if (ptr >= max)
        throw new OverflowIntStackException();
    return stk[ptr++] = x;
}
```

- ptr >= max를 하는 이유 <br>
  프로그래밍 실수와 같은 원인으로 max를 초과할 수 있는데 그 문제를 막아주어서 프로그램의 안정성을 높일 수 있다.

#### 📍 pop 메소드

가장 마지막에 push된 값을 지워주는 메소드이다.

```java
public int pop() throws EmptyIntStackException {
    if (ptr <= 0)
        throw new EmptyIntStackException();
    return stk[--ptr];
}
```

#### 📍 peek 메소드👀

스택의 꼭대기에 있는 데이터를 **몰래 엿보는** 메소드이다.

```java
public int peek() throws EmptyIntStackException {
    if (ptr <= 0)
        throw new EmptyIntStackException();
    return stk[ptr - 1];
}
```

#### 📍 indexOf 메소드

스택 본체의 배열 stk에 x와 같은 값의 데이터가 포함되어 있는지, 포함되어 있다면 배열의 어디에 들어 있는지를 조사하는 메소드이다. 검색에 성공하면 요소의 인덱스를 반환하고, 실패하면 -1을 반환한다.

```java
public int indexOf(int x) {
    for (int i = ptr - 1; i >= 0; i--) {
        if (stk[i] == x)
            return i;
    }
    return -1;
}
```

#### 📍 clear 메소드

스택에 쌓여 있는 모든 데이터를 삭제하는 메소드이다.

```java
public void clear() {
    ptr = 0;
}
```

#### 📍 capacity 메소드

스택의 용량을 반환하는 메소드이다.

```java
public int capacity() {
    return max;
}
```

#### 📍 size 메소드

현재 채워져 있는 데이터의 수를 반환하는 메소드이다.

```java
public int size() {
    return ptr;
}
```

#### 📍 isEmpty 메소드

스택이 비어 있는지 검사하는 메소드이다.

```java
public boolean isEmpty() {
    return ptr <= 0;
}
```

#### 📍 isFull 메소드

스택이 가득 찼는지 검사하는 메소드이다.

```java
public boolean isFull() {
    return ptr >= max;
}
```

#### 📍 dump 메소드

모든 데이터를 바닥부터 꼭대기 순으로 출력하는 메소드이다.

```java
public void dump() {
    if (ptr <= 0) {
        System.out.println("스택이 비어있습니다.");
    } else {
        for (int i = 0; i < ptr; i++) {
            System.out.print(stk[i] + " ");
        }
        System.out.println();
    }
}
```

## ➕연결 리스트로 stack 구현

### 📖 인터페이스

```java
interface DStack {
    boolean isEmpty();
    boolean isFull();
    void push(Object data);
    void pop();
    void peek();
    void clear();
}
```

### 📍 생성자

- 노드

  ```java
  class Node {
      Object data;
      Node next;

      public Node() {
          this.data = null;
          this.next = null;
      }

      public Node(Object data) {
          this.data = data;
          this.next = null;
      }

      public Object getData() {
          return this.data;
      }
  }
  ```

- 스택

  ```java
  public class ListStack implements DStack {
  Node head;
  Node top;
  int stackSize; // 배열의 개수

  public ListStack(int size) {
      this.head = null;
      this.top = null;
      stackSize = size;
  }
  ```

  - head : 머리 노드
  - top : 마지막 노드
  - stackSize : 스택의 노드 개수

### 📍 isEmpty()

```java
public boolean isEmpty() {
    return null == top;
}
```

### 📍 isFull()

```java
public boolean isFull() {
    if (isEmpty()) {
        return false;
    } else {
        int nodeCount = 0;
        Node ptr = top;
        while (ptr.next != null) {
            ++nodeCount;
            ptr = ptr.next;
        }
        return this.stackSize - 1 == nodeCount;
    }
}
```

빈 스택이 아니라면 노드 개수를 센다. <br>
❓ 현재 노드의 개수를 세서 stackSize == max로 조건문을 쓸 수는 없을까?

### 📍 push()

```java
public void push(Object data) {
    Node node = new Node();
    if (isFull()) {
        System.out.println("Stack is Full");
        return;
    } else if (isEmpty()) {
        this.head = node;
        this.top = this.head;
    } else {
        Node ptr = top;
        while (ptr.next != null) {
            ptr = ptr.next;
        }
        ptr.next = node;
    }
}
```

빈 스택이었다면 head와 top을 모두 수정해주어야 한다. 하지만 빈 스택이 아니라면 마지막 노드에 링크를 연결한다. <br>
❓ top이 마지막 노드라면 `top.next = node;` 로 해주면 안되나?

### 📍 pop()

```java
public void pop() {
    if (isEmpty()) {
        System.out.println("Stack is Empty");
        return;
    }
    // 스택에 노드가 한 개 남았을 경우
    else if (top.next == null) {
        top = null;
        head = null;
    } else {
        Node ptr = top.next;
        Node pre = top;
        while (ptr.next != null) {
            pre = ptr;
            ptr = ptr.next;
        }
        pre.next = null;
    }
}
```

❓ head = null ,,,?
❗ 굳이 while문을 돌리면서 마지막 노드까지 가는 이유는 마지막 노드의 전 노드를 알기 위해서다. 그래야 마지막 노드의 전 노드를 null과 연결시키지

### 📍 peek()

```java
public void peek() {
    if (isEmpty()) {
        System.out.println("Stack is Empty");
        return;
    } else {
        Node ptr = top;
        while (ptr.next != null) {
            ptr = ptr.next;
        }
        System.out.println(ptr.getData());
    }
}
```

❓ 마지막 노드가 top이라면 굳이? 그냥 peek.data로 하면 되는 거 아닌가? 그리고 왜 getData가 필요하지?

### 📍 clear()

```java
public void clear() {
    if (isEmpty()) {
        System.out.println("Stack is Empty");
        return;
    }
    head = null;
    top = null;
}
```
