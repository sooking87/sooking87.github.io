---
title: "[JAVA] 큐"
excerpt: "큐"
categories: [Algorithm Study]
tags: [Algorithm Study, Java, Algorithm]
toc: true
toc_sticky: true
published: true
---

## ✨ 큐

### 📖 큐란?

스택과 마찬가지로 데이터를 일시적을 쌓아 두기 위한 자료구조이다. 가장 먼저 넣은 데이터를 가장 먼저 꺼내는 **선입선출** 구조이다.

#### 📍 링 버퍼로 큐 만들기

링 버서는 배열의 처음이 끝과 연결되어있는 자료구조이다. 그렇기 때문에 첫 요소와 마지막 요소를 식별하기 위해서 front, rear 필드를 사용한다.

```java
package QUEUE;

public class IntQueue {
    private int max; // 큐 용량
    private int front; // 첫 번째 요소 커서
    private int rear; // 마지막 요소 커서
    private int num; // 현재 데이터 수
    private int[] que; // 큐 본체

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
    public IntQueue(int capacity) {
        num = front = rear = 0;
        max = capacity;
        try {
            que = new int[max];
        } catch (OutOfMemoryError e) {
            max = 0;
        }
    }
```

- max: 큐 용량을 저장하는 필드
- front: 첫 번째 요소 커서의 인덱스를 저장하는 필드
- rear: 인큐한 데이터 가운데 맨 나중에 넣은 요소의 하나 뒤의 인덱스를 저장하는 필드
- num: 현재 데이터 수를 나타내는 필드
- que: 큐 본체

#### 📍 enque 메소드

큐에 데이터를 인큐하는 메소드이다.

```java
// 큐에 데이터를 인큐
public int enque(int x) throws OverflowIntQueueException {
    if (num >= max) {
        throw new OverflowIntQueueException();
    }
    que[rear++] = x;
    num++;
    if (rear == max)
        rear = 0;
    return x;
}
```

인큐에 성공하면 인큐한 값을 그대로 반환한다. 근데 만약에 rear++을 한 다음 if문으로 들어갔을 때, if문의 조건이 성립하는 경우가 있을 수 있다. 이를 대비하기 위해서 rear을 배열의 처음인 0으로 변경한다. 지금 링 버퍼를 사용하고 있기 때문에 가능!

#### 📍 deque 메소드

큐에서 데이터를 디큐하고 그 값을 반환하는 메소드이다.

```java
public int deque() throws EmptyIntQueueException {
    if (num <= 0)
        throw new EmptyIntQueueException();
    int x = que[front++];
    num--;
    if (front == max)
        front = 0;
    return x;
}
```

deque도 마찬가지로 front++을 하고 if문의 조건이 성립할 수 있다. 그래서 `front = 0;` 을 통해서 이를 보완하였다.

#### 📍 peek 메소드

맨 앞의 데이터를 몰래 엿보는 메소드이다.

```java
// 큐에서 데이터를 피크
public int peek() throws EmptyIntQueueException {
    if (num <= 0)
        throw new EmptyIntQueueException();
    return que[front];
}
```

#### 📍 indexOf 메소드

큐의 배열에서 x와 같은 데이터가 저장되어 있는 위치를 알아내는 메소드이다.

```java
// 큐에서 x를 검색하여 인덱스를 반환
public int indexOf(int x) {
    for (int i = 0; i < num; i++) {
        int idx = (i + front) % max;
        if (que[idx] == x)
            return idx;
    }
    return -1;
}
```

스캔의 시작은 배열의 첫 요소가 아니라 큐의 첫 요소, 즉 프런트이다. 그래서 스캔할 때 주목하는 인덱스 idx의 계산이 (i + front) % max로 복잡하다...

#### 📍 clear 메소드

```java
// 큐를 비움
public void clear() {
    num = front = rear = 0;
}
```

#### 📍 capacity 메소드

```java
// 큐의 용량을 반환
public int capacity() {
    return max;
}
```

#### 📍 size 메소드

```java
// 큐에 쌓여 있는 데이터 수를 반환
public int size() {
    return num;
}
```

#### 📍 isEmpty 메소드

```java
// 큐가 비어있나요?
public boolean isEmpty() {
    return num <= 0;
}
```

#### 📍 isFull 메소드

```java
// 큐가 가득 차있나요?
public boolean isFull() {
    return num >= max;
}
```

#### 📍 dump 메소드

```java
public void dump() {
    if (num <= 0) {
        System.out.println("큐가 비어있습니다.");
    } else {
        for (int i = 0; i < num; i++) {
            System.out.println(que[(i + front) % max] + " ");
        }
        System.out.println();
    }
}
```
