---
title: "[백준 2480번] 주사위 세개"
excerpt: "[백준 2480번] 주사위 세개"
categories: [Algorithm Java]
tags: [Algorithm Study, Java, Algorithm, Backjoon]
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

public class backjoon_2480 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int first = Integer.parseInt(st.nextToken());
        int second = Integer.parseInt(st.nextToken());
        int last = Integer.parseInt(st.nextToken());
        int[] nums = { first, second, last };
        int money = 0;

        Arrays.sort(nums); // 배열 정렬하기

        if (nums[0] == nums[1]) {
            if (nums[1] == nums[2]) {
                money = 10000 + nums[0] * 1000;
            } else {
                money = 1000 + nums[0] * 100;
            }
        } else if (nums[1] == nums[2]) {
            money = 1000 + nums[1] * 100;
        } else {
            money = nums[2] * 100;
        }
        System.out.println(money);
    }
}
```

## 문제 풀이

정렬 후 주사위의 숫자 비교를 했다. 그 방법이 비교하기도 쉽고, 가장 큰 주사위 값을 구하기에도 쉽기 때문이다.
