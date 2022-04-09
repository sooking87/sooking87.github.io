---
title: "[백준 2869번] 달팽이는 올라가고 싶다. "
excerpt: "[백준 2869번] 달팽이는 올라가고 싶다. "
categories: [Backjoon Java]
tags: [Backjoon, Java]
toc: true
toc_sticky: true
---

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class backjoon_2869 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int a = Integer.parseInt(st.nextToken());
        int b = Integer.parseInt(st.nextToken());
        int v = Integer.parseInt(st.nextToken());

        int ans = (int) Math.ceil((v - b) / (double) (a - b));
        System.out.println(ans);
    }
}
```

## 풀이

a만큼 정상에 올라가면 stop이므로 일단 내려올 만큼 빼주고 a - b를 나누고, 마지막날 하루 올라간 만큼을 더해주기 위해서 올림을 사용. (높이에서 밤에 미끄러지는 높이)인 높이까지만 올라가면 다음날 정상에 도착 가능(Math.ceil) <br>
⭐ 자바에서는 형 변환 주의!! -> Math.ceil(double a)이므로 괄호 안의 값은 double형이여야 되므로 명시적 형변환을 해주었고, 정답은 int형이므로 마찬가지로 Math.ceil를 통해 나온 값(double형)에서 명시적으로 int형으로 바꾸어 주었다.
