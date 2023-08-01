---
title: "[백준 24052번] 삽입 정렬"
excerpt: "[백준 24052번] 삽입 정렬"
categories: [Algorithm Java]
tags: [Algorithm Study, Java, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

# 알고리즘 수업 - 삽입 정렬 2

## 문제

오늘도 서준이는 삽입 정렬 수업 조교를 하고 있다. 아빠가 수업한 내용을 학생들이 잘 이해했는지 문제를 통해서 확인해보자.

N개의 서로 다른 양의 정수가 저장된 배열 A가 있다. 삽입 정렬로 배열 A를 오름차순 정렬할 경우 배열 A의 원소가 K 번 변경된 직후의 배열 A를 출력해 보자.

크기가 N인 배열에 대한 삽입 정렬 의사 코드는 다음과 같다.

insertion_sort(A[1..N]) { # A[1..N]을 오름차순 정렬한다.

```java
    for i <- 2 to N {
        loc = i - 1;
        newItem = A[i];

        # 이 지점에서 A[1..i-1]은 이미 정렬되어 있는 상태
        while (1 <= loc and newItem < A[loc]) {
            A[loc + 1] <- A[loc];
            loc--;
        }
        if (loc + 1 != i) then A[loc + 1] = newItem;
    }
}
```

## 입력

첫째 줄에 배열 A의 크기 N(5 ≤ N ≤ 10,000), 변경 횟수 K(1 ≤ K ≤ N2)가 주어진다.

다음 줄에 서로 다른 배열 A의 원소 A1, A2, ..., AN이 주어진다. (1 ≤ Ai ≤ 109)

## 출력

K 번 변경이 발생한 직후의 배열 A를 한 줄에 출력한다. 변경 횟수가 K 보다 작으면 -1을 출력한다.

## 예제 입력 1

```
5 7
4 5 1 3 2
```

## 예제 출력 1

```
1 3 4 5 5
```

4 5 1 3 2 -> 4 5 5 3 2 -> 4 4 5 3 2 -> 1 4 5 3 2 -> 1 4 5 5 2 -> 1 4 4 5 2 -> 1 3 4 5 2 -> 1 3 4 5 5 -> 1 3 4 4 5 -> 1 3 3 4 5 -> 1 2 3 4 5. 총 10회 변경이 발생하고 일곱 번째 변경 직후 배열 A이 모습은 1 3 4 5 5이다.

## 예제 입력 2

```
5 11
4 5 1 3 2
```

## 예제 출력 2

```
-1
```

## 📌 문제 풀이

```java
package InsertionSort;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.util.StringTokenizer;

public class backjoon_24052 {
    static boolean insertionSort(int[] arr, int n, int k) {
        int cnt = 0;
        for (int i = 1; i < n; i++) {
            int j;
            int temp = arr[i];
            for (j = i; j > 0 && arr[j - 1] > temp; j--) {
                arr[j] = arr[j - 1];
                cnt++;

                if (cnt == k) {
                    return true;
                }
            }
            //순서가 바뀐 경우에만 temp를 넣어준 후 cnt++
            if (j != i) {
                arr[j] = temp;
                cnt++;
                if (cnt == k) {
                    return true;
                }
            }
        }
        return false;
    }

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        StringTokenizer st;
        st = new StringTokenizer(br.readLine());

        int n = Integer.parseInt(st.nextToken()); // 배열 개수
        int k = Integer.parseInt(st.nextToken()); // k번 변경
        int[] arr = new int[n];
        st = new StringTokenizer(br.readLine());

        for (int i = 0; i < n; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }

        if (insertionSort(arr, n, k)) {
            for (int i = 0; i < n; i++) {
                bw.write(arr[i] + " ");
            }
            System.out.println();
        } else {
            System.out.println(-1);
        }
        bw.close();
    }
}
```
