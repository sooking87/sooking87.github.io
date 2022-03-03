---
title: "[백준 2331번] 반복 수열"
excerpt: "[백준 2331번] 반복 수열"
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
import java.util.ArrayList;
import java.util.List;
import java.util.StringTokenizer;

public class 백준_손수경_정답_2331 {
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int a = Integer.parseInt(st.nextToken());
        int p = Integer.parseInt(st.nextToken());

        List<Integer> list = new ArrayList<>();
        list.add(a);

        while (true) {
            int temp = list.get(list.size() - 1);
            int result = 0;

            while (temp != 0) {
                result += (int)Math.pow(temp % 10, (double)p); 
                temp /= 10;
            }

            if (list.contains(result)) {
                int ans = list.indexOf(result);
                bw.write(ans + "\n");
                break;
            }

            list.add(result);
        }

        bw.close();
    }
}
```

## 풀이 방법

**.contains()** 메서드를 활용해야되므로 리스트를 만들어주었다. 수열을 규칙대로 만들어가다가 이 수가 리스트에 포함되어 있다면, 그 수의 인덱스 값만큼이 반복되지 않은 수의 개수가 된다. 인덱스는 0부터 시작하기 때문.