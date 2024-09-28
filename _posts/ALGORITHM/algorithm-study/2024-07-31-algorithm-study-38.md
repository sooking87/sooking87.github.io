---
title: "[C/C++] O(NlogN) 정렬, 기초수학, 약수와 배수, 소수"
excerpt: "[C/C++] O(NlogN) 정렬, 기초수학, 약수와 배수, 소수"
categories: [Algorithm Study]
tags: [Algorithm Study, C/C++, Algorithm]
toc: true
toc_sticky: true
published: true
---

## 합병 정렬

![머지소트](https://blog.kakaocdn.net/dn/dI3rqm/btrhdVWZmU6/kwGd83V3MEoCQdHlLK0UQ0/img.gif)

## 힙 정렬

![힙정렬](https://velog.velcdn.com/images/pso0301/post/f391cd33-b539-499f-ac51-eb875f9c532b/image.gif)

## 퀵 소트

![퀵소트](https://user-images.githubusercontent.com/48043799/145678758-65e11c13-ba5b-4553-80ee-2c1dfb4175d3.gif)

## 나머지 구하기

`(A+B)%C는 ((A%C) + (B%C))%C` 는 같다. 

왜 ? 

![mod](assets/image/Algorithm-Study/mod.png)

## 유클리드 호제법

```cpp
// 유클리드 호제법
int divide(long long int num1, long long int num2) {
    if (num1 % num2 == 0) {
        return num2;
    }
    else {
        return divide(num2, num1 % num2);
    }
}
```