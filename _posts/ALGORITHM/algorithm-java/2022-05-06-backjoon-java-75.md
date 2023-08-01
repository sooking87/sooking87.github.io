---
title: "[백준 24389번] 2의 보수 "
excerpt: "[백준 24389번] 2의 보수 "
categories: [Algorithm Java]
tags: [Algorithm Study, Java, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

```java
package Week5_1;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class backjoon_24389 {
    static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

    public static void main(String[] args) throws IOException {
        // 입력
        int inputNum = Integer.parseInt(br.readLine());
        // 비트 반전 후 1 더하기
        int outputNum = ~inputNum + 1;
        // XOR 연산
        int sameBitNum = inputNum ^ outputNum;
        // 서로 다른 비트 수 카운트
        int count = 0;

        for (char ch : Integer.toBinaryString(sameBitNum).toCharArray()) {
            System.out.println(ch);
            if (ch == '1') {
                count++;
            }
        }
        // 출력
        System.out.print(count);
    }
}
```

## 풀이

- ~ 연산자 : 반전 연산자
- ^ 연산자 : xor 연산자로 비교하는 비트가 다르면 1, 같으면 0
- Integer.toBinaryString(int) : 10진수 -> 2진수(32비트로~)
