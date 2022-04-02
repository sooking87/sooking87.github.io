---
title: "❗ [백준 1874번] 스택 ❗"
excerpt: "❗ [백준 1874번] 스택 ❗"
categories: [Algorithm Java, Backjoon Java]
tags: [Algorithm Study, Java, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

## 문제

스택 (stack)은 기본적인 자료구조 중 하나로, 컴퓨터 프로그램을 작성할 때 자주 이용되는 개념이다. 스택은 자료를 넣는 (push) 입구와 자료를 뽑는 (pop) 입구가 같아 제일 나중에 들어간 자료가 제일 먼저 나오는 (LIFO, Last in First out) 특성을 가지고 있다.

1부터 n까지의 수를 스택에 넣었다가 뽑아 늘어놓음으로써, 하나의 수열을 만들 수 있다. 이때, 스택에 push하는 순서는 반드시 오름차순을 지키도록 한다고 하자. 임의의 수열이 주어졌을 때 스택을 이용해 그 수열을 만들 수 있는지 없는지, 있다면 어떤 순서로 push와 pop 연산을 수행해야 하는지를 알아낼 수 있다. 이를 계산하는 프로그램을 작성하라.

## 입력

첫 줄에 n (1 ≤ n ≤ 100,000)이 주어진다. 둘째 줄부터 n개의 줄에는 수열을 이루는 1이상 n이하의 정수가 하나씩 순서대로 주어진다. 물론 같은 정수가 두 번 나오는 일은 없다.

## 출력

입력된 수열을 만들기 위해 필요한 연산을 한 줄에 한 개씩 출력한다. push연산은 +로, pop 연산은 -로 표현하도록 한다. 불가능한 경우 NO를 출력한다.

## 예제 입력 1

```
8
4
3
6
8
7
5
2
1
```

## 예제 출력 1

```
+
+
+
+
-
-
+
+
-
+
+
-
-
-
-
-
```

## 예제 입력 2

```
5
1
2
5
3
4
```

## 예제 출력 2

```
NO
```

## 힌트

1부터 n까지에 수에 대해 차례로 [push, push, push, push, pop, pop, push, push, pop, push, push, pop, pop, pop, pop, pop] 연산을 수행하면 수열 [4, 3, 6, 8, 7, 5, 2, 1]을 얻을 수 있다

## 문제 풀이

```java
package STACK;

import java.util.Scanner;
import java.util.Stack;

public class backjoon_1874 {
    private int max;
    private int ptr;
    private int[] stk;

    public backjoon_1874(int capacity) {
        ptr = 0;
        max = capacity;
        stk = new int[max];
    }

    public boolean isEmpty() {
        return ptr <= 0;
    }

    public boolean isFull() {
        return ptr >= max;
    }

    public void push(int data) {
        if (isFull()) {
            System.out.println("Stack is Full");
            return;
        }
        stk[ptr] = data;
        ptr++;
    }

    public int pop() {
        if (isEmpty()) {
            System.out.println("Stack is Empty");
            return -1;
        }
        ptr--;
        return stk[ptr];
    }

    public int peek() {
        if (isEmpty()) {
            System.out.println("Stack is Empty");
            return -1;
        }
        return stk[ptr - 1];

    }

    public void print() {
        for (int i = 0; i < max; i++) {
            System.out.print(stk[i]);
        }
        System.out.println();
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        StringBuilder ans = new StringBuilder();
        int n = sc.nextInt();
        backjoon_1874 stack = new backjoon_1874(n);
        int top = 0;
        for (int i = 0; i < n; i++) {
            int num = sc.nextInt();
            if (num > top) {
                for (int j = top + 1; j <= num; j++) {
                    stack.push(j);
                    ans.append("+\n");
                }
                top = num;
                System.out.println("peek: " + stack.peek());
                System.out.println("nums: " + num);
            } else if (stack.peek() != num) {
                System.out.println("NO");
                return;
            }
            stack.print();
            stack.pop();
            ans.append("-\n");
        }
        System.out.println(ans);

    }
}
```

## 풀이

pop되는 값이 입력받은 순서대로 되야되는 문제이다. +, -로 출력되는 값은 이해를 했지만, NO가 출력되는 규칙이 이해가 안됨.. 나중에 다시 볼 것 !
