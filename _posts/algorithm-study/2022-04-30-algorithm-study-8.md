---
title: "[JAVA] 버블 정렬"
excerpt: "버블 정렬"
categories: [Algorithm Study]
tags: [Algorithm Study, Java, Algorithm]
toc: true
toc_sticky: true
published: true
---

## 🔮 버블 정렬

![download4](https://user-images.githubusercontent.com/96654391/165982551-6bd7b521-8865-4db6-8899-421d1d11a55f.gif)

버블 정렬이란 서로 인접한 두 데이터를 검사하여 정렬하는 알고리즘입니다.

### 📍 기본 버블 정렬

**_sol 1. 뒤에서부터 비교하는 방법_**

```java
// 맨 뒤 원소부터 정렬하는 방법
for (int i = 0; i < n - 1; i++) {
    for (int j = n - 1; j > i; j--) {
        if (a[j - 1] > a[j]) {
            swap(a, j - 1, j);
        }
    }
}
```

- i : 몇 번째 인덱스까지 비교할 것인지
- j : 몇 번째 인덱스부터 비교할 것인지 <br>

j번 째 요소부터 비교를 통해서 i번째 요소까지 비교를 한다. 즉, 뒤에서부터 앞에 있는 요소와 비교를 통해서 앞에 있는 요소(a[j - 1])가 뒤에 있는 요소(a[j])보다 크다면 swap 함수를 통해서 순서를 바꾼다. **결국 정렬을 맨 앞에서부터 이루어 진다.**
<br>

**_sol 2. 앞에서부터 비교하는 방법_**

```java
// 맨 앞 원소부터 정렬하는 방법
for (int i = 0; i < n - 1; i++) {
    for (int j = i; j < n - 1; j++) {
        if (a[j] > a[j + 1]) {
            swap(a, j, j + 1);
        }
    }
}
```

- i : 몇 번째 인덱스부터 비교할 것인지
- j : 몇 번째 인덱스까지 비교할 것인지 <br>

i번째 요소부터 j번째 요소까지 비교를 한다. 즉, 앞에서부터 뒤에 있는 요소와 비교를 해서 앞에 있는 요소가 뒤에 있는 요소보다 크다면 swap 함수를 통해서 요소 위치를 바꾼다. **결국 정렬을 맨 앞에서부터 이루어 진다.**
<br> <br>

❗ 문제점 : 더 이상 요소의 교환이 필요없더라도 반드시 반복문을 모두 돌아야 한다. = 비효율 ❗ <br>

### 💡 알고리즘 개선 1

더이상의 교환이 없을 경우, 반복문을 종료시킨다.

```java
// 맨 뒤 원소부터 정렬하는 방법
for (int i = 0; i < n - 1; i++) {
    int exchg = 0;
    for (int j = n - 1; j > i; j--) {
        if (a[j - 1] > a[j]) {
            swap(a, j - 1, j);
            exchg++;
        }
    }
    if (exchg == 0) break;
}
```

- exchg : 교환이 일어난 횟수를 계산한다.

### 💡 알고리즘 개선 2

last를 통해서 a[last] 앞의 요소들은 모두 정렬되었음을 확인시켜 준다.

```java
int k = 0;
while (k < n - 1) {
    int last = n - 1;
    for (int j = n - 1; j > k; j--) {
        if (a[j - 1] > a[j]) {
            swap(a, j - 1, j);
            last = j;
        }
    }
    k = last;
}
```

Ex 1. {22, 5, 11, 32, 21} : <br>

- k = 0 -> last = 1
- k = 1 -> last = 2
- k = 2 -> last = 3
- k = 3 -> last = 4 -> break <br>

▶️ 이런 배열이라면 기존 버블 정렬과 별로 차이점은 없다. 하지만 다음 배열에서는 굉장히 효과 적임을 볼 수 있다. <br>

Ex 2. {1, 4, 11, 32, 21} : <br>

- k = 0 -> last = 4 -> break <br>

## 🔮 결론

결론적으로 버블 정렬을 바로 옆에 있는 요소와 비교를 통해서 정렬된 요소의 개수를 하나씩 늘려나가는 방식이다. 개선 알고리즘들은 모두 **기존에 정렬되어 있던 요소는 바꾸지 않는 방식** 으로 진행하였다.
