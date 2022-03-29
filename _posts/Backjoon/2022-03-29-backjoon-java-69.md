---
title: "[백준 1588번] 곱셈"
excerpt: "[백준 1588번] 곱셈"
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

public class backjoon_2588_sol2 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int num1 = Integer.parseInt(br.readLine());
        String num2 = br.readLine();
        for (int i = num2.length() - 1; i >= 0; i--) {
            int temp = Integer.parseInt(Character.toString(num2.charAt(i))) * num1;
            System.out.println(temp);
        }
        System.out.println(num1 * Integer.parseInt(num2));
    }
}
```

## 문제 풀이

입력받은 데이터 타입은 문자열인데, 여기서 일의 자리부터 하나씩 숫자를 뽑아서 num1과 곱하기 위해서 charAt 메소드를 생각했다. 하지만 Integer.parseInt() 메소드의 경우 문자열만 정수형으로 바꾸어주므로 다시 문자열로 바꾸고 parseInt를 통해서 정수형으로 바꾸어 주었다.
