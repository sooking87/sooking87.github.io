---
title: "[JAVA] 이분 탐색"
excerpt: "이분 탐색"
categories: [Algorithm Study]
tags: [Algorithm Study, Java, Algorithm]
toc: true
toc_sticky: true
published: true
---

## 🔮 이분 탐색

이분 탐색(Binary Search)란 이미 정렬되어 있는 배열에서 데이터를 찾으려고 시도할 때, 탐색 범위를 절반씩 줄여가면서 찾아가는 탐색 방법이다. 이 방법은 데이터 구조 시간에 특정 숫자를 찾는 탐색하는 방법을 배울 때 배웠던 알고리즘이다. 
![Untitled](https://user-images.githubusercontent.com/96654391/174749069-cecbd517-355b-45e5-b1e3-7f6af20603ea.png) 

### 📍 이분 탐색 코드

```java
public static int binarySearch(int key) {
    int start = 0;
    int end = arr.length - 1;

    while (start <= end) {
        int mid = (start + end) / 2;
        if (key < arr[mid]) {
            end = mid - 1;
        } else if (key > arr[mid]) {
            start = mid + 1;
        } else {
            return mid;
        }
    }
    return -1;
}
```

