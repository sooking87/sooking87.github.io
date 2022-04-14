---
title: "[백준 9047번] 6174 "
excerpt: "[백준 9047번] 6174 "
categories: [Backjoon Java]
tags: [Backjoon, Java]
toc: true
toc_sticky: true
---

```java
package src.Week4_1;

import java.util.Arrays;
import java.util.Collections;
import java.util.Scanner;

public class backjoon_9047 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        for (int i = 0; i < n; i++) {
            String num = sc.next();
            int cnt = 0;
            while (true) {
                if (num.compareTo("6174") == 0) {
                    break;
                }
                String[] str = num.split("");
                String[] str2 = num.split("");
                Arrays.sort(str); // 오름 차순
                Arrays.sort(str2, Collections.reverseOrder()); // 내림 차순
                int min = Integer.parseInt(String.join("", str));
                int max = Integer.parseInt(String.join("", str2));
                num = Integer.toString(max - min);
                if (num.length() != 4) {
                    if (num.length() == 3) {
                        num = "0" + num;
                    } else if (num.length() == 2) {
                        num = "00" + num;
                    } else {
                        num = "000" + num;
                    }
                }
                cnt++;
            }
            System.out.println(cnt);

        }
    }
}
```

## 풀이

sort(), sort(str, Collections.reverseOrder())을 통해서 오름차순, 내림차순을 만들고 String.join() 메소드를 사용하여서 배열을 문자열로 만들었다. 그런 다음 규칙대로 max - min으로 만들어주고 네 자리 수를 맞춰야되기 때문에 길이가 4인지 아닌지를 통해서 문자열에 '0'을 붙혀주었다.

- Arrays.sort(배열) : 오름차순으로 정렬시켜 준다.
- Arrays.sort(배열, Collections.reverseOrder()) : 내립차순으로 정렬시켜 준다.
- String.join("", 배열) : ""안에 문자를 기준으로 배열의 요소들을 붙혀준다.
