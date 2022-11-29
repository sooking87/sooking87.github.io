---
title: "[백준 1158번] 원형 리스트"
excerpt: "[백준 1158번] 원형 리스트"
categories: [Algorithm Java, Backjoon Java]
tags: [Algorithm Study, Java, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

## 문제

요세푸스 문제는 다음과 같다.

1번부터 N번까지 N명의 사람이 원을 이루면서 앉아있고, 양의 정수 K(≤ N)가 주어진다. 이제 순서대로 K번째 사람을 제거한다. 한 사람이 제거되면 남은 사람들로 이루어진 원을 따라 이 과정을 계속해 나간다. 이 과정은 N명의 사람이 모두 제거될 때까지 계속된다. 원에서 사람들이 제거되는 순서를 (N, K)-요세푸스 순열이라고 한다. 예를 들어 (7, 3)-요세푸스 순열은 < 3, 6, 2, 7, 5, 1, 4>이다.

N과 K가 주어지면 (N, K)-요세푸스 순열을 구하는 프로그램을 작성하시오.

## 입력

첫째 줄에 N과 K가 빈 칸을 사이에 두고 순서대로 주어진다. (1 ≤ K ≤ N ≤ 5,000)

## 출력

예제와 같이 요세푸스 순열을 출력한다.

## 예제 입력 1

```
7 3

```

## 예제 출력 1

```
<3, 6, 2, 7, 5, 1, 4>
```

## 📌 풀이

```java

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

//2
public class DbLinkedListTest<E> {
		//1
    class Node<E> {
        private E data;
        private Node<E> prev;
        private Node<E> next;

        Node() {
            data = null;
            prev = next = this;
        }

        Node(E obj, Node<E> prev, Node<E> next) {
            data = obj;
            this.prev = prev;
            this.next = next;
        }
    }

    private Node<E> head;
    private Node<E> crnt;

    public DbLinkedListTest() {
        head = crnt = new Node<E>(); // 더미 노드
    }

		//3
    public boolean isEmpty() {
        return head.next == head;
    }
                        /* 원형 이중 연결 리스트 set */

		//5
    public void add(E obj) {
        Node<E> node = new Node<E>(obj, crnt, crnt.next);
        crnt.next = crnt.next.prev = node;
        crnt = node;
        // System.out.print("add ");
        // printAll();
    }

		//7
    public void remove(Node<E> crnt) {
        if (!isEmpty()) {
            crnt.prev.next = crnt.next;
            crnt.next.prev = crnt.prev;
            crnt = crnt.prev;

            // System.out.print("remove ");
            // printAll();
        }
    }

		//6
    public E moveK(int range) {
        int cnt = 0;
        Node<E> ptr = crnt.next;
        // System.out.println("moveK, ptr.data " + ptr.data);
        while (cnt != range - 1) {
            if (ptr == head) { // head가 가리키는 노드는 더미 노드 이므로 카운트 하지 않음
                System.out.println("moveK, ptr == head " + ptr.data);
                ptr = ptr.next;
                continue;
            }
            System.out.println("moveK, ptr != head " + ptr.data);
            cnt++;
            ptr = ptr.next;
        }
        crnt = ptr;
        if (crnt == head) {
            crnt = crnt.next;
        }
        System.out.println(crnt.data);
        remove(crnt);
        return crnt.data;
    }

    public void printAll() {
        Node<E> ptr = head.next;
        System.out.print("<");
        while (ptr.next != head) { // 꼬리 노드 전까지 출력
            System.out.print(ptr.data + ", ");
            ptr = ptr.next;
        }
        System.out.println(ptr.data + ">");
    }

		//4
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        DbLinkedListTest<Integer> list = new DbLinkedListTest<>();
        DbLinkedListTest<Integer> printList = new DbLinkedListTest<>();
        int n = Integer.parseInt(st.nextToken());
        int k = Integer.parseInt(st.nextToken());

        for (int i = 1; i <= n; i++) {
            list.add(i);
        }

				//6
        for (int i = 0; i < n; i++) {
            int num = list.moveK(k);
            printList.add(num);
        }
        printList.printAll();
    }

}
```

## 📌 풀이 과정

add 메소드를 통해서 1부터 N까지의 숫자를 리스트에 넣고, 문제의 규칙대로 수행하는 moveK 메소드를 만들었습니다. crnt의 위치에 따라서 원형 리스트의 모든 메소드들을 정의해놓았기 때문에 모든 메소드는 현재 수정한 값을 기준으로 뒤쪽 노드 또는 현재 노드를 crnt로 수정해놓는 코드가 꼭 필요합니다.

## 📌 ADT

- add(E obj) : 입력받은 값을 리스트에 넣기 위한 메소드이다.
- remove(Node`<`E`>` crnt) : crnt를 지워주는 메소드이다.
- moveK(int range) : range만큼 뒤쪽으로 이동시켜줍니다. 이동시 주의해야 될 점은 더미 노드는 카운트를 해서는 안된다는 점이다.

  ```java
  if (ptr == head) { // head가 가리키는 노드는 더미 노드 이므로 카운트 하지 않음
      System.out.println("moveK, ptr == head " + ptr.data);
      ptr = ptr.next;
      continue;
  }
  ```

  여기서 어려웠던 것 역시 crnt.next이냐 crnt이냐의 문제,,,열심히 그려가면서 구했던 것 같다.

- printAll() : 모든 노드를 출력해주는 메소드이다. 여기서 중요하게 봐야될 것은 `ptr.next != head` 라는 조건문이다. 원형 리스트이기 때문에 어디가 마지막인지 null을 통해서 알 수 없다. 그리고 `ptr = ptr.next` 이거 안넣으면 ㅋㅋㅋ 무한대로 출력 ㅋㅋ ❗
