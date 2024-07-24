---
title: "[백준 2747] 피보나치수"
excerpt: "[백준 2747] 피보나치수"
categories: [Algorithm C_C++]
tags: [Algorithm Study, C/C++, Algorithm]
toc: true
toc_sticky: true
---

DP: 구현방법으로는 Bottom-up과 Top-down이 있다. 풀이 차이는 아래 코드로! 

뭔가 반복적인 계산이 필요한 경우 DP를 사용하고, 작은 문제들을 한 번씩 풀고 어딘가(배열)에 적어두는 식으로 풀어가는 방식

📌 [백준 2747 문제 링크](https://www.acmicpc.net/problem/2747) <br>

## 백준 2747 피보나치수

## 풀이 코드

### Bottom-up

```c
#include <iostream>
using namespace std;

int fibo(int n) {
    int first = 0;
    int second = 1;
    int next = 0;

    if (n <= 1) {
        return n;
    }
    for (int i = 2; i <= n; i++) {
        next = first + second;
        first = second;
        second = next;
    }
    return next;
}

int main() {
    int n;
    cin >> n;
    cout << fibo(n) << '\n';
}
```

## 코드 설명

bottom up은 작은 부분부터 하나하나 하는 것이기 때문에 코드를 보면 반복문을 돌리면서 i가 2일 때 부터 진행을 하는 것을 확인할 수 있다.

### Top Down

- 10870 피보나치수 5

```c
#include <iostream>
using namespace std;

int arr[22] = {0, };
int fibo(int n) {
    if (arr[n] > 0) {
        return arr[n];
    }
    if (n <= 1) {
        return n;
    }
    else {
        arr[n] = fibo(n - 1) + fibo(n - 2);
        return arr[n];
    }
}
int main() {
    int n;
    cin >> n;
    cout << fibo(n) << '\n';
}
```

이 코드를 보면 n이 클 때부터 재귀적으로 코드를 풀이해나가고 있다. Top Down이 많이 쓰인다고는 한다! 뭔가 반복적인 계산이 필요한 경우 DP를 사용하고, 작은 문제들을 한 번씩 풀고 어딘가(배열)에 적어두는 식으로 풀어가는 방식