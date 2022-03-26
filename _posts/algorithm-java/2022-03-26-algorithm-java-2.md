---
title: "[백준 2346번] 원형 리스트"
excerpt: "[백준 2346번] 원형 리스트"
categories: [Algorithm Java, Backjoon Java]
tags: [Algorithm Study, Java, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

## 문제

1번부터 N번까지 N개의 풍선이 원형으로 놓여 있고. i번 풍선의 오른쪽에는 i+1번 풍선이 있고, 왼쪽에는 i-1번 풍선이 있다. 단, 1번 풍선의 왼쪽에 N번 풍선이 있고, N번 풍선의 오른쪽에 1번 풍선이 있다. 각 풍선 안에는 종이가 하나 들어있고, 종이에는 -N보다 크거나 같고, N보다 작거나 같은 정수가 하나 적혀있다. 이 풍선들을 다음과 같은 규칙으로 터뜨린다.

우선, 제일 처음에는 1번 풍선을 터뜨린다. 다음에는 풍선 안에 있는 종이를 꺼내어 그 종이에 적혀있는 값만큼 이동하여 다음 풍선을 터뜨린다. 양수가 적혀 있을 경우에는 오른쪽으로, 음수가 적혀 있을 때는 왼쪽으로 이동한다. 이동할 때에는 이미 터진 풍선은 빼고 이동한다.

예를 들어 다섯 개의 풍선 안에 차례로 3, 2, 1, -3, -1이 적혀 있었다고 하자. 이 경우 3이 적혀 있는 1번 풍선, -3이 적혀 있는 4번 풍선, -1이 적혀 있는 5번 풍선, 1이 적혀 있는 3번 풍선, 2가 적혀 있는 2번 풍선의 순서대로 터지게 된다.

## 입력

첫째 줄에 자연수 N(1 ≤ N ≤ 1,000)이 주어진다. 다음 줄에는 차례로 각 풍선 안의 종이에 적혀 있는 수가 주어진다. 종이에 0은 적혀있지 않다.

## 출력

첫째 줄에 터진 풍선의 번호를 차례로 나열한다.

## 예제 입력 1

```
5
3 2 1 -3 -1
```

## 예제 출력 1

```
1 4 5 3 2
```

## 문제 풀이

노드의 데이터를 출력하는 것이 아니라 인덱스를 출력하는 문제이기 때문에 커서로 만든 연결 리스트를 통해서 해볼 예정,,,,이었으나 커서로 만든 연결 리스트에서 값을 중간에 추가하는 방법을 모르겠음,,,,,그래서! 원형 이중 연결 리스트를 통해서 풀었다. 인덱스를 출력해야되므로 인덱스도 노드에 같이 넣어주었다. 그래서 노드는 **data, index, crnt, crnt.next>** 이렇게 추가하였다.

```java
package LIST;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class backjoon_2346<E> {
    // 노드
    class Node<E> {
        private E data;
        private int index;
        private Node<E> prev;
        private Node<E> next;

        // Node<E> 생성자
        Node() {
            data = null;
            prev = next = this;
        }

        // Node<E> 생성자
        Node(E obj, int idx, Node<E> prev, Node<E> next) {
            data = obj;
            index = idx;
            this.prev = prev;
            this.next = next;
        }
    }

    private Node<E> head;
    private Node<E> crnt;

    public backjoon_2346() {
        head = crnt = new Node<E>(); // 더미 노드
    }

    public boolean isEmpty() {
        return head.next == head;
    }

    public void add(E obj, int index) {
        Node<E> node = new Node<E>(obj, index, crnt, crnt.next);
        crnt.next = crnt.next.prev = node;
        crnt = node;
    }

    public void remove() {
        int data = (int) crnt.data;
        crnt.prev.next = crnt.next;
        crnt.next.prev = crnt.prev;
        crnt = crnt.prev;
        move(data);
    }

    public void setFirst() {
        Node<E> ptr = crnt;
        System.out.println(1);
        ptr = ptr.next.next;
        crnt = ptr;

        System.out.println("setRemoveData, crnt.data: " + crnt.data);
        remove();

    }

    public void move(int data) {
        int absData = data < 0 ? -data : data;
        System.out.println("data: " + data + ", absData: " + absData);
        Node<E> ptr = crnt;
        int cnt;

        // remove메소드에서 crnt로 설정해놓은 것이 지운 것보다 앞쪽 노드이므로 지운 노드의 데이터가 음수라면 한번 적게 이동시켜야됨
        if (data == absData) {
            cnt = 0;
        } else {
            cnt = 1;
        }

        while (cnt != absData) {
            if (data == absData) {
                ptr = ptr.next;
                if (ptr == head) {
                    ptr = ptr.next;
                }
            } else {
                ptr = ptr.prev;
                if (ptr == head) {
                    ptr = ptr.prev;
                }
            }
            System.out.println("move, ptr.data: " + ptr.data);
            cnt++;
        }
        crnt = ptr;
        System.out.println(crnt.index);
    }

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        int n = Integer.parseInt(br.readLine());
        int index = 1;
        backjoon_2346<Integer> list = new backjoon_2346<>();
        st = new StringTokenizer(br.readLine());

        for (int i = 0; i < n; i++) {
            int temp = Integer.parseInt(st.nextToken());
            list.add(temp, index);
            index++;
        }

        // 처음에 무조건 1번 풍선부터 터트리기 때문에 setFirst를 통해서 1번 풍선은 터트리고 시작하므로 n - 1번만 반복문 돌리면 됨
        for (int i = 0; i < n - 1; i++) {
            if (i == 0) {
                list.setFirst();
            } else {
                list.remove();
            }
        }
    }
}
```


## ADT

- add(E obj, int index) : 입력된 값을 넣어준다. 여기서 인덱스도 같이 넣어주었다. 인덱스를 출력해야되는 문제기 때문이다.

- remove() : crnt를 지워주는 메소드이다.

- move(int data) : 이 문제 해결의 가장 큰 비중을 차지하고 있는 메소드이다. 중요한 것은 remove함수에서 crnt로 결정되는 노드는 지워진 노드의 앞쪽 노드( _crnt = crnt.prev_ )이기 때문에 만약에 지워진 노드의 데이터가 음수였다면 실제보다 1번 덜 앞으로 가야된다.

  ```java
  if (data == absData) {
      cnt = 0;
  } else {
      cnt = 1;
  }
  ```

remove 메소드를 통해서 이미 앞쪽 노드가 한 칸 이동했기 때문이다.
