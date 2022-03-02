---
title: "[백준 11586번] 지영 공주님의 마법 거울"
excerpt: "[백준 11586번] 지영 공주님의 마법 거울"
categories: [Backjoon Java]
tags: [Backjoon, Java]
toc: true
toc_sticky: true
---

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class 백준_손수경_정답_11586 {
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        String[][] mirror = new String[n][n];

        for (int i = 0; i < n; i++) {
            String temp = br.readLine();
            mirror[i] = temp.split("");
        }

        int k = Integer.parseInt(br.readLine());
        if (k == 1) {
            for (int i = 0; i < n; i++) {
                for (String j : mirror[i]) {
                    System.out.print(j);
                }
                System.out.println();
            }
        }
        else if (k == 2) {
            for (int i = 0; i < n; i++) {
                for (int j = n - 1; j >= 0; j--) {
                    System.out.print(mirror[i][j]);
                }
                System.out.println();
            }
        }
        else {
            for (int i = n - 1; i >= 0; i--) {
                for (int j = 0; j < n; j++) {
                    System.out.print(mirror[i][j]);
                }
                System.out.println();
            }
        }
    }
}
```

## 풀이 방법

1이 입력되면 입력받은 값 그대로 출력, 2가 입력되면 좌우 반전 후 출력, 3이 입력되면 상하 반전 후 출력해준다. 
여기서 이차원 배열일 경우, 각 행에 대해서 split 메서드를 사용하는 방법는 다음과 같다. 

```java
Stirng[][] arr = new String[n][n];
for (int i = 0; i < n; i++) {
    String temp = br.readLine();
    arr[i] = temp.split("");
}
```

행에 대한 인덱스값만 넣어주고, split처리해주면 된다. 