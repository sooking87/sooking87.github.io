---
title: "[JAVA] 정렬 / 선택 정렬"
excerpt: "정렬 / 선택 정렬"
categories: [Algorithm Study]
tags: [Algorithm Study, Java, Algorithm]
toc: true
toc_sticky: true
published: true
---

## 🔮 정렬

정렬은 이름, 학번, 키 등 핵심 항목(key)의 대소 관계에 따라 데이터 집합을 일정한 순서로 줄지어 늘어서도록 바꾸는 작업을 말한다.

- 정렬 알고리즘의 핵심 요소
  - 교환
  - 선택
  - 삽입

## 🔮 단순 선택 정렬

단순 선택 정렬은 가장 작은 요소부터 선택해 알맞은 위치로 옮겨서 순서대로 정렬하는 알고리즘이다.

### 📍 진행 과정

배열 중 하나를 기준으로 반복문을 돌면서 기준값 이후의 요소들 중 가장 작은 값을 기준 위치와 바꾼다.

```java
static void selectionSort(int[] a, int n) {
    for (int i = 0; i < n - 1; i++) {
        int min = i;
        for (int j = i + 1; j < n; j++) {
            if (a[j] < a[min]) {
                min = j;
            }
        }
        swap(a, i, min);
    }
}
```

```java
static void swap(int[] a, int i, int j) {
    int temp = a[i];
    a[i] = a[j];
    a[j] = temp;
}
```

💡 활용 <br>

```java
int[] num = { 5, 3, 6, 2, 1, 4 };
selectionSort(num, num.length);
```

출력값

1. 536214
2. 136254
3. 126354
4. 123654
5. 123456
6. 123456
