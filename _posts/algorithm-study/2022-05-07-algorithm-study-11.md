---
title: "[JAVA] 퀵 정렬"
excerpt: "퀵 정렬"
categories: [Algorithm Study]
tags: [Algorithm Study, Java, Algorithm]
toc: true
toc_sticky: true
published: true
---

## 🔮 퀵 정렬

말 그대로 정렬 속도가 매우 빠르다.

### 📍 Partition

```java
package QuickSort;

import java.util.Scanner;

public class Partition {
    static void swap(int[] a, int idx1, int idx2) {
        int t = a[idx1];
        a[idx1] = a[idx2];
        a[idx1] = t;
    }

    // 배열을 나눕니다.
    static void partition(int[] a, int n) {
        int pl = 0;
        int pr = n - 1;
        int x = a[n / 2];

        do {
            // 피벗보다 큰 값의 인덱스(pl)를 가진 상태로 반복문 종료
            while (a[pl] < x)
                pl++;
            // 피벗보다 작은 값의 인덱스(pr)를 가진 상태로 반복문 종료
            while (a[pr] > x)
                pr--;

            if (pl <= pr) {
                swap(a, pl++, pr--);
            }
        } while (pl <= pr);
    }
}
```

![download3](https://user-images.githubusercontent.com/96654391/167243283-9bb95599-f84d-49d5-bf02-f4728a544155.png)
<br>

이런 느낌으로 진행 <br>

피벗 기준 왼쪽 배열에서 피벗보다 큰 경우를 a[pl]이고, 피벗 기준 오른쪽 배열에서 피벗보다 작은 경우가 a[pr]이다. -> 이거 둘의 위치를 바꾸고 다음 인덱스부터 다시 반복문 시작! <br>

1. 피벗을 하나 선택한다.

2. 피벗을 기준으로 양쪽에서 피벗보다 큰 값, 혹은 작은 값을 찾는다. 왼쪽에서부터는 피벗보다 큰 값을 찾고, 오른쪽에서부터는 피벗보다 작은 값을 찾는다.

3. 양 방향에서 찾은 두 원소를 교환한다.

4. 왼쪽에서 탐색하는 위치와 오른쪽에서 탐색하는 위치가 엇갈리지 않을 때 까지 2번으로 돌아가 위 과정을 반복한다.

5. 엇갈린 기점을 기준으로 두 개의 부분리스트로 나누어 1번으로 돌아가 해당 부분리스트의 길이가 1이 아닐 때 까지 1번 과정을 반복한다. (Divide : 분할)

6. 인접한 부분리스트끼리 합친다. (Conqure : 정복)

<br> <br>

얘를 발전시키면 퀵 정렬 알고리즘이 된다.

### 📍 재귀적 퀵 정렬

```java
package QuickSort;

import java.util.Scanner;

public class QuickSort {
    static void swap(int[] a, int idx1, int idx2) {
        int t = a[idx1];
        a[idx1] = a[idx2];
        a[idx2] = t;
    }

    // 퀵 정렬
    static void quickSort(int[] a, int left, int right) {
        int pl = left;
        int pr = right;
        int x = a[(pl + pr) / 2]; // 피벗

        /* 실행 과정 살펴보기 */
        System.out.printf("a[%d]~a[%d] : {", left, right);
        for (int i = left; i < right; i++) {
            System.out.print(a[i] + " ");
        }
        System.out.printf("%d}\n", a[right]);

        do {
            while (a[pl] < x)
                pl++;
            while (a[pr] > x)
                pr--;

            if (pl <= pr) {
                swap(a, pl++, pr--);
            }
        } while (pl <= pr);

        if (left < pr)
            quickSort(a, left, pr);
        if (pl < right)
            quickSort(a, pl, right);
    }
}
```

- left : 배열 시작 요소의 인덱스
- right : 배열 끝 요소의 인덱스
- pl : 배열의 시작 요소부터 시작해서 오른쪽으로 이동하면서 피벗 요소 전까지 배열 요소 정렬에 사용
- pr : 배열의 끝 요소부터 시작해서 왼쪽으로 이동하면서 피벗 요소 다음까지 배열 요소 정렬

> 입력 : int[] a = {5, 8, 4, 2, 6, 1, 3, 9, 7}

> 실행 과정 : <br>

    a[0]~a[8] : {5 8 4 2 6 1 3 9 7} <br>
    a[0]~a[4] : {5 3 4 2 1} <br>
    a[0]~a[2] : {1 3 2} <br>
    a[0]~a[1] : {1 2} <br>
    a[3]~a[4] : {4 5} <br>
    a[5]~a[8] : {6 8 9 7} <br>
    a[5]~a[6] : {6 7} <br>
    a[7]~a[8] : {9 8}

실행 과정을 보면 왼쪽 배열부터 먼저 진행 -> 그 후 오른쪽 배열이 진행되는 것을 알 수 있다. <br>
왜! WHY? <br>

```java
if (left < pr)
    quickSort(a, left, pr);
if (pl < right)
    quickSort(a, pl, right);
```

이 코드 때문! 그리고 이 코드의 조건식에 의해서 1개 배열은 조건문에 해당되지 않고 함수를 끝냄 = 즉, 2개 이상의 그룹만을 나누는 퀵 정렬 실행이 가능

### 📍 비재귀적 퀵 정렬

chap 04 stack에서의 코드 재사용 ⬇️

```java
/* chap 04 stack */
class IntStack {
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

    public boolean isEmpty() {
        return ptr <= 0;
    }

    public int push(int x) throws OverflowIntStackException {
        if (ptr >= max)
            throw new OverflowIntStackException();
        return stk[ptr++] = x;
    }

    public int pop() throws EmptyIntStackException {
        if (ptr <= 0)
            throw new EmptyIntStackException();
        return stk[--ptr];
    }
}
```

<br>

비재귀적 퀵 정렬 구현 ⬇️

```java
public class UnrecursiveQuickSort {
    static void swap(int[] a, int idx1, int idx2) {
        int t = a[idx1];
        a[idx1] = a[idx2];
        a[idx2] = t;
    }

    static void quickSort(int[] a, int left, int right) {
        IntStack lstack = new IntStack(right - left + 1);
        IntStack rstack = new IntStack(right - left + 1);

        lstack.push(left);
        rstack.push(right);

        while (lstack.isEmpty() != true) {
            int pl = left = lstack.pop();
            int pr = right = rstack.pop();
            int x = a[(left + right) / 2];

            do {
                while (a[pl] < x)
                    pl++;
                while (a[pr] > x)
                    pr--;

                if (pl <= pr) {
                    swap(a, pl++, pr--);
                }
            } while (pl <= pr);

            if (left < pr) {
                lstack.push(left);
                rstack.push(pr);
            }

            if (pl < right) {
                lstack.push(pl);
                rstack.push(right);
            }
        }
    }
}
```

- lstack : 배열의 시작 인덱스를 넣는 스택
- rstack : 배열의 끝 인덱스를 넣는 스택
- pl : 배열의 시작 요소부터 시작해서 오른쪽으로 이동하면서 피벗 요소 전까지 배열 요소 정렬에 사용
- pr : 배열의 끝 요소부터 시작해서 왼쪽으로 이동하면서 피벗 요소 다음까지 배열 요소 정렬

### 📍 퀵 정렬에서 고려 사항

#### 1️⃣ 스택의 용량(only 비재귀적 퀵 정렬에서만 해당)

1. 요소의 개수가 많은 그룹을 **_먼저_** 푸시하는 경우
2. 요소의 개수가 적은 그룹을 **_먼저_** 푸시하는 경우 <br>

일반적으로 요소의 개수가 적은 배열일수록 분할 해야되는 횟수가 적으므로 요소의 개수가 적은 그룹부터 정렬하고 그 다음 요소의 개수가 많은 배열을 정렬하는 것 하는 것이 좋다. <br>
사실 시간 복잡도 상으로는 큰 차이는 없지만 스택에 push, pop 되는 개수에서 차이가 난다. -> Do it 알고리즘 p.238 그림 참고

#### 2️⃣ 피벗 선택

피벗을 선택하는 방법에 따라 퀵 정렬의 실행 효율에 큰 영향을 미친다. <br>

- 왼쪽 피벗 선택
- 오른쪽 피벗 선택
- 중간 피벗 선택 <br>
  <https://st-lab.tistory.com/250> 참고

### 📍 시간 복잡도

퀵 정렬이 왜 빠른가? <br>
요소의 개수가 1이 될 때까지 쪼개면서 정렬을 하기 때문 <br>

- 시간 복잡도 : O(n\*log n), 최대 O(n<sup>2</sup>)

## 🔮 정렬 정리
