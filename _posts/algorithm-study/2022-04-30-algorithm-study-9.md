---
title: "[JAVA] 삽입 정렬"
excerpt: "삽입 정렬"
categories: [Algorithm Study]
tags: [Algorithm Study, Java, Algorithm]
toc: true
toc_sticky: true
published: true
---

## 🔮 삽입 정렬

단순 삽입 정렬은 선택한 요소를 그보다 더 앞쪽의 알맞은 위치에 **_삽입하는_** 작업을 반복하여 정렬하는 알고리즘이다.

![download3](https://user-images.githubusercontent.com/96654391/166097108-b633ba6f-c50d-461d-9473-9abba961bb61.png)

이런 느낌으로 코드가 진행된다. 위 예시를 봤을 때, temp가 자신의 위치를 찾기 전까지 반복문을 돌리면서 요소를 한 칸씩 뒤로 미룬다. (a[j] = a[j - 1]) 그리고 temp의 위치를 찾으면 그 위치에 temp를 넣어준다. (a[j] = temp)

```java
static void insertionSort(int[] a, int n) {
    for (int i = 1; i < n; i++) {
        int j;
        int temp = a[i];
        // 반복문을 돌면서 temp가 들어갈 자리를 찾는다.
        for (j = i; j > 0 && a[j - 1] > temp; j--) {
            a[j] = a[j - 1]; // 한 칸 오른쪽으로 이동
        }
        // temp가 들어갈 자리에 temp값을 넣어준다.
        a[j] = temp;
    }
}
```

앞에서 공부했던 세 가지 단순 정렬인 **_버블 정렬_**, **_선택 정렬_**, **_삽입 정렬_** 의 시간 복잡도는 모두 **_O(n^2)_** 입니다. 이를 개선하기 위해서는 셸 정렬과 퀵 정렬이 있습니다.
