---
title: "[백준 5063번] TGN"
excerpt: "[백준 5063번] TGN"
categories: [Backjoon Java]
tags: [Backjoon, Java]
toc: true
toc_sticky: true
---

```java
import java.util.Scanner;

public class 백준_손수경_정답_5063 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();

        for (int i = 0; i < n; i++) {
            int r = sc.nextInt();
            int e = sc.nextInt();
            int c = sc.nextInt();

            if (r > e - c) {
                System.out.println("do not advertise");
            }
            else if (r < e - c) {
                System.out.println("advertise");
            }
            else {
                System.out.println("does not matter");
            }
        }
    }
}
```

## 풀이 방법

광고를 하지 않았을 때의 이익과 광고를 했을 때 이익 - 광고 비의 비교에 따라서 원하는 출력값을 출력해주면 된다. 