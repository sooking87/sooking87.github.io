---
title: "[백준 1145번] 적어도 대부분의 배수"
excerpt: "[백준 1145번] 적어도 대부분의 배수"
categories: [Backjoon Java]
tags: [Backjoon, Java]
toc: true
toc_sticky: true
---

```java
package Week3_5;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.StringTokenizer;

public class backjoon_1145 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int[] arr = new int[5];
        for (int i = 0; i < 5; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }
        Arrays.sort(arr);
        int cnt = 0;
        int min = arr[0];
        while (true) {
            for (int i = 0; i < arr.length; i++) {
                if (min % arr[i] == 0) {
                    cnt++;
                }
            }
            if (cnt >= 3) {
                break;
            }
            cnt = 0;
            min++;
        }
        System.out.println(min);
    }
}
```

## 문제 풀이

입력된 수는 100을 넘지 않는다고 하였으므로 최소를 100으로 두고 최솟값을 잡는다. 그런다음 최솟값부터 1씩 늘려가면서 나누어 떨어지는 값이 3개 이상이 될때까지 반복문을 돌린다.
