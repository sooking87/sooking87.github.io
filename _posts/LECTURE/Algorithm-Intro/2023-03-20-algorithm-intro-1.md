---
title: "Chap 01. 알고리즘 개요"
excerpt: "Chap 01. 알고리즘 개요"
categories: [Algorithm Intro]
tags: [Algorithm Intro, Python]
toc: true
toc_sticky: true
---

## 실습 1

```py
# IT공학전공 2116313 손수경
# 1번을 해보세요!
a = int(input())
b = int(input())

# 2번을 해보세요!


def gcd(a, b):
    while b != 0:
        r = a % b
        a = b
        b = r
    return a


# 출력합니다!
print("%d, %d의 최대 공약수 =" % (a, b), gcd(a, b))

```

## 실습 2

```py
# IT공학전공 2116313 손수경
# 1번을 해보세요!
def find_max(A):
    max = A[0]
    # for i in range(1, len(A)):
    #     temp = A[i]
    #     if temp > max:
    #         max = temp
    for i in A[1:]:
        if i > max:
            max = i
    return max


# 2번을 해보세요!
array = [int(n) for n in input().split()]

# 출력합니다!
print(array, "최댓값=", find_max(array))

```
