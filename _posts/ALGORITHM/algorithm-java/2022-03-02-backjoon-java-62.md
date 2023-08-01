---
title: "[백준 1551번] 수열의 변화"
excerpt: "[백준 1551번] 수열의 변화"
categories: [Algorithm Java]
tags: [Algorithm Study, Java, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class 백준_손수경_정답_1551 {
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        st = new StringTokenizer(br.readLine());
        int n = Integer.parseInt(st.nextToken());
        int k = Integer.parseInt(st.nextToken());
        String temp = br.readLine();
        String[] aString = temp.split(",");
        int[] aInt = new int[n];
        for (int i = 0; i < n; i++) {
            aInt[i] = Integer.parseInt(aString[i]);
        }
        int[] before = aInt;
        for (int i = 0; i < k; i++) {
            before = getArr(before, n - 1, i);
        }
        for (int i = 0; i < before.length; i++) {
            if (i >= 0 && i < before.length - 1) {
                System.out.print(before[i] + ",");
            }
            else {
                System.out.println(before[i]);
            }
        }
    }

    public static int[] getArr(int[] before, int size, int i) {
        size -= i;
        int[] after = new int[size];
        for (int j = 0; j < size; j++) {
            after[j] = before[j + 1] - before[j];
        }
        return after;
    }
}
```

## 풀이 방법

`getArr`이라는 메서드를 만들어서 `a[i + 1] - a[i]`이라는 규칙을 적용시켰다. 여기서 중요한 점은 k번 만큼 규칙을 적용시키는 것이다. 처음에 입력받은 숫자들을 넣은 배열로 초기화 시킨 배열과, 반복할 횟수를 넣는다. 그리고 거기서 리턴되는 값을 다시 매개변수 배열로 대입시켜서 k번 돌아가게 하였다.
