---
title: "[백준 10989번] 퀵 정렬"
excerpt: "[백준 10989번] 퀵 정렬"
categories: [Algorithm Java]
tags: [Algorithm Study, Java, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

## 문제

N개의 수가 주어졌을 때, 이를 오름차순으로 정렬하는 프로그램을 작성하시오.

## 입력

첫째 줄에 수의 개수 N(1 ≤ N ≤ 10,000,000)이 주어진다. 둘째 줄부터 N개의 줄에는 수가 주어진다. 이 수는 10,000보다 작거나 같은 자연수이다.

## 출력

첫째 줄부터 N개의 줄에 오름차순으로 정렬한 결과를 한 줄에 하나씩 출력한다.

## 예제 입력 1

```
10
5
2
3
1
4
2
3
5
1
7
```

## 예제 출력 1

```
1
1
2
2
3
3
4
5
5
7
```

## 📌 문제 풀이

```java
package QuickSort;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class backjoon_10989 {
    static void swap(int[] a, int idx1, int idx2) {
        int t = a[idx1];
        a[idx1] = a[idx2];
        a[idx2] = t;
    }

    // 퀵 정렬
    static void quickSort(int[] a, int left, int right) {

        /* 실행 과정 살펴보기 */
        System.out.printf("a[%d]~a[%d] : {", left, right);
        for (

                int i = left; i < right; i++) {
            System.out.print(a[i] + " ");
        }
        System.out.printf("%d}\n", a[right]);
        int pl = left;
        int pr = right;
        int x = a[(pl + pr) / 2]; // 피벗

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

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        int[] nums = new int[n];

        for (int i = 0; i < n; i++) {
            nums[i] = Integer.parseInt(br.readLine());
        }

        quickSort(nums, 0, n - 1);

        for (int i = 0; i < n; i++) {
            System.out.println(nums[i]);
        }

    }

}
```

퀵 정렬 정리 부분의 코드와 거의 동일!

## 📌 정답 풀이

```java
package QuickSort;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.util.Arrays;

public class submit {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        int n = Integer.parseInt(br.readLine());
        int[] nums = new int[n];

        for (int i = 0; i < n; i++) {
            nums[i] = Integer.parseInt(br.readLine());
        }

        Arrays.sort(nums);

        for (int i = 0; i < n; i++) {
            bw.write(nums[i] + "\n");
        }

        bw.close();
    }
}
```

정답이 될려면 역시 sort 메소드 사용이 필요하다... + BufferedReader와 BufferedWriter도.....
