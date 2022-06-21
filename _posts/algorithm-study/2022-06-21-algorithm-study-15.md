---
title: "[JAVA] 힙 정렬"
excerpt: "힙 정렬"
categories: [Algorithm Study]
tags: [Algorithm Study, Java, Algorithm]
toc: true
toc_sticky: true
published: true
---

## 🔮 힙 정렬이란

힙 정렬은 힙을 사용하여 정렬하는 알고리즘이다. 여기서 힙은 **_부모의 값이 자식의 값보다 항상 크다_** 는 조건을 만족하는 완전이진트리이다. 이를 Max-HIP 이라고 한다. **_부모의 값이 자식보다 항상 작아도 힙_** 이라고 하고, 이를 Min-HIP 이라고 한다.

### 📍 힙 정렬 과정

1. 루트 힙을 없애고 마지막 노드를 루트로 이동
2. 다시 힙 상태를 유지하도록 만들어줌
3. 이때, 자식의 값이 작거나 잎에 다다르면 작업 종료 <br>

시간 복잡도: O(n log n)

### 📍 배열로 힙 만들기

```java
package HeapSort;

import java.util.Scanner;

public class HeapSort {
    static void swap(int[] a, int idx1, int idx2) {
        int t = a[idx1];
        a[idx1] = a[idx2];
        a[idx2] = t;
    }

    // a[left] ~ a[right]를 힙으로 만듭니다.
    static void downHeap(int[] a, int left, int right) {
        int temp = a[left]; // 루트
        int child;
        int parent;

        for (parent = left; parent < (right + 1) / 2; parent = child) {
            int cl = parent * 2 + 1; // 왼쪽 자식
            int cr = cl + 1;
            child = (cr <= right && a[cr] > a[cl]) ? cr : cl; // 큰 값을 가진 노드를 자식에 대입
            if (temp >= a[child]) {
                break;
            }
            a[parent] = a[child];
        }
        a[parent] = temp;
    }

    // 힙 정렬
    static void heapSort(int[] a, int n) {
        // 처음 Max 힙 만드는 과정
        for (int i = (n - 1) / 2; i >= 0; i--) {
            downHeap(a, i, n - 1);
        }

        // 제일 마지막 노드와 첫 노드를 바꾸어준 후, 루트노드부터 힙을 만드는 반복문
        for (int i = n - 1; i > 0; i--) {
            swap(a, 0, i); // 가장 큰 요소와 아직 정렬되지 않은 부분의 마지막 요소를 교환
            downHeap(a, 0, i - 1); // a[0] ~ a[i-1]을 힙으로 만들어줌.
        }
    }

    public static void main(String[] args) {
        Scanner stdIn = new Scanner(System.in);

        System.out.println("힙 정렬");
        System.out.printf("요솟수: ");
        int nx = stdIn.nextInt();
        int[] x = new int[nx];

        for (int i = 0; i < nx; i++) {
            System.out.printf("x[" + i + "]: ");
            x[i] = stdIn.nextInt();
        }

        heapSort(x, nx);

        System.out.println("오름차순 정렬 완료");
        for (int i = 0; i < nx; i++) {
            System.out.println("x[" + i + "]=" + x[i]);
        }
    }
}
```
### 📍 함수 설명

- swap() : idx1과 idx2에 해당하는 값을 바꾸어 준다. 
- downHeap() : a[left] ~ a[right] 까지 힙으로 만든다. 
- heapSort() : 힙 정렬로 바꾸어 준다. 반복문 2개를 포함하고 있는데 첫 번째 반복문의 경우는 입력받은 배열을 힙 정렬로 만드는 과정이다. 그 다음 두 번째 반복문을 통해서 루트 노드와 잎 노드를 바꾸고 힙 정렬을 하는 과정을 다루고 있다. 
