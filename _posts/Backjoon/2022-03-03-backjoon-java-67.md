---
title: "[백준 2331번] 카드2"
excerpt: "[백준 2331번] 카드2"
categories: [Backjoon Java]
tags: [Backjoon, Java]
toc: true
toc_sticky: true
---

```java
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.util.LinkedList;

public class 백준_손수경_정답_2164 {
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        int n = Integer.parseInt(br.readLine());
        LinkedList<Integer> cards = new LinkedList<>();
        
        for (int i = 1; i <= n; i++) {
            cards.add(i);
        }
        
        while (cards.size() != 1) {
            cards.removeFirst();
            cards.addLast(cards.get(0));
            cards.removeFirst();
        }
        
        bw.write(cards.get(0) + "\n");
        bw.close();
    }
}
```

## 풀이 방법

이 문제는 리스트에 대하여 수정해야될 부분이 많기 때문에 ArrayList보다는 LinkedList가 편리할 것으로 생각되어 LinkedList를 사용하였다. 문제 규칙대로 n까지의 숫자를 리스트에 넣은 다음 첫 번째 요소 버리고, 그 다음 요소를 제일 뒤로 보내고, 이것을 `cards`에 요소 1개가 남아있을 때까지 수행한다. 