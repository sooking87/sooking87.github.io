---
title: "[백준 11931번] 버블 정렬"
excerpt: "[백준 11931번] 버블 정렬"
categories: [Algorithm Java, Backjoon Java]
tags: [Algorithm Study, Java, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

## 문제

N개의 수가 주어졌을 때, 이를 내림차순으로 정렬하는 프로그램을 작성하시오.

## 입력

첫째 줄에 수의 개수 N(1 ≤ N ≤ 1,000,000)이 주어진다. 둘째 줄부터 N개의 줄에는 숫자가 주어진다. 이 수는 절댓값이 1,000,000보다 작거나 같은 정수이다. 수는 중복되지 않는다.

## 출력

첫째 줄부터 N개의 줄에 내림차순으로 정렬한 결과를 한 줄에 하나씩 출력한다.

## 예제 입력 1

```text
5
1
2
3
4
5
```

## 예제 출력 1

```
5
4
3
2
1
```

## 문제 풀이

```java
package BubbleSort;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class backjoon_11931 {
    public static void swap(int[] arr, int idx1, int idx2) {
        int t = arr[idx1];
        arr[idx1] = arr[idx2];
        arr[idx2] = t;
    }

    public static void bubbleSort(int[] arr, int n) {
        for (int i = 0; i < n - 1; i++) {
            int exchg = 0;
            for (int j = 0; j < n - i - 1; j++) {
                if (arr[j] < arr[j + 1]) {
                    swap(arr, j, j + 1);
                    exchg++;
                }
            }

            if (exchg == 0)
                break;
        }
    }

    public static void printAll(int[] arr, int n) {
        for (int j = 0; j < n; j++) {
            System.out.println(arr[j]);
        }
    }

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        int[] arr = new int[n];

        // 배열 요소 입력받기
        for (int i = 0; i < n; i++) {
            int temp = Integer.parseInt(br.readLine());
            arr[i] = temp;
        }

        bubbleSort(arr, n);

        printAll(arr, n);
    }
}
```

-> 이 문제를 채점해보면 계속 시간 초과 문제가 뜬다. 백준에서 요구하는 정렬 방식이 버블 정렬이 아니라서 그런 것 같다. 하지만 버블 정렬에 대한 문제 예제이므로 버블 정렬로 문제를 풀었다.

## 정답 풀이

```java
package BubbleSort;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.util.Arrays;
import java.util.Collections;

public class ForSubmit {

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        int n = Integer.parseInt(br.readLine());
        Integer[] arr = new Integer[n];

        // 배열 요소 입력받기
        for (int i = 0; i < n; i++) {
            int temp = Integer.parseInt(br.readLine());
            arr[i] = temp;
        }

        Arrays.sort(arr, Collections.reverseOrder());

        for (Integer i : arr) {
            bw.write(i + "\n");
        }
        bw.close();
    }
}
```

❗ 반드시 BufferedReader와 BufferedWriter를 사용해주어야 시간 초과 문제가 발생하지 않는다. ❗
