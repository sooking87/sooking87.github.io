---
title: "[백준 17388번] 와글와글 숭고한"
excerpt: "[백준 17388번] 와글와글 숭고한"
categories: [Backjoon Java]
tags: [Backjoon, Java]
toc: true
toc_sticky: true
---

```java
import java.util.Scanner;

public class 백준_손수경_정답_17388 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int S = sc.nextInt();
        int K = sc.nextInt();
        int H = sc.nextInt();
        int min = Math.min(H, Math.min(S, K));
        if (S + K + H >= 100) {
            System.out.println("OK");
        }
        else {
            if (min == S) {
                System.out.println("Soongsil");
            }
            else if (min == K) {
                System.out.println("Korea");
            }
            else {
                System.out.println("Hanyang");
            }
        }
    }
}
```

## 풀이 방법

참여도 중 가장 작은 학교를 구하기 위해서 `Math` 클래스의 **min** 메서드를 사용해 주었다. 그런 다음 가장 작은 참여도에 해당하는 학교를 출력하는 방식으로 진행하였다. 