---
title: "[C++] 괄호 회전하기"
categories: [Programmers Java]
tags: [Programmers, Java]
excerpt: "[C++] 괄호 회전하기"
toc: true
toc_sticky: true
---

## 문제

<https://school.programmers.co.kr/learn/courses/30/lessons/76502>

## 최대 공약수

```cpp
// 최대 공약수
void postDiv(int &denum, int &num)
{
    int div = 0;
    int min = denum > num ? num : denum;

    for (int i = min; i > 0; i--)
    {
        if (denum % i == 0 && num % i == 0)
        {
            div = i;
            break;
        }
    }

    denum /= div;
    num /= div;
}
```
