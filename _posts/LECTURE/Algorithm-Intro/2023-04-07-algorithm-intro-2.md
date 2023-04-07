---
title: "4.1주차"
excerpt: "4.1주차"
categories: [Algorithm Intro]
tags: [Algorithm Intro, Python]
toc: true
toc_sticky: true
---

## 실습 1

```py
# IT공학전공 2116313 손수경
# 1번을 해보세요!
def sequential_search(A, key):
    for i in range(len(A)):
        if A[i] == key:
            return i
    return -1


# 2번을 해보세요!
A = [int(n) for n in input().split()]
key = int(input())

# 출력합니다!
print("%d찾기:" % (key), sequential_search(A, key))

```

## 실습 2

```py
# IT공학전공 2116313 손수경
# 1번을 해보세요!
def compute_square_A(n):
    return n * n


# 2번을 해보세요!
n = int(input())

# 출력합니다!
print(compute_square_A(n))

```

## 실습 3

```py
# IT공학전공 2116313 손수경
# 1번을 해보세요!
def compute_square_B(n):
    sum = 0
    # 복잡도가 O(n)이 되도록 반복문을 작성해보세요!
    for i in range(n):
        sum += n
    return sum


# 2번을 해보세요!
n = int(input())

# 출력합니다!
print(compute_square_B(n))

```

## 실습 4

```py
# IT공학전공 2116313 손수경
# 1번을 해보세요!
def compute_square_C(n):
    sum = 0
    # 복잡도가 O(n^2)이 되도록 이중 for 문을 작성해보세요!
    for i in range(n):
        for j in range(n):
            sum += 1
    return sum


# 2번을 해보세요!
n = int(input())

# 출력합니다!
print(compute_square_C(n))

```

## 실습 5

```py
# IT공학전공 2116313 손수경
# 1번을 해보세요!
A = [int(n) for n in input().split()]

# 2번을 해보세요!


def unique_elements(A):
    for i in range(len(A)):
        for j in range(i + 1, len(A)):
            if A[i] == A[j]:
                return False
    return True


# 출력합니다!
print(unique_elements(A))

```

교수님 코드 ⏬

```py
# 2116313 손수경
# 1번을 해보세요!
A = [int(n) for n in input().split()]

# 2번을 해보세요!


def unique_elements(A):
    n = len(A)
    for i in range(n - 1):
        for j in range(i + 1, n):
            if A[i] == A[j]:
                return False
    return True


# 출력합니다!
print(unique_elements(A))
```

## 실습 6

```py
# IT공학전공 2116313 손수경
# 1번을 해보세요!
def binary_digits(n):
    count = 1
    while n > 1:
        count += 1
        n = n // 2
    return count


# 2번을 해보세요!
n = int(input())

# 출력합니다!
print(binary_digits(n))

```

다른 방법 ⏬ <br>
나눠서 구하는 것이 아니라 result에서 2씩 곱해가면서 n보다 크거가 같아지는 횟수를 구하는 식으로 생각할 수 있다.

```py
def binary_digits(n):
    k = 1
    cnt = 0
    while k <= n:
        cnt += 1
        k *= 2
    return cnt


n = int(input())

print(binary_digits(n))
```

## 실습 7

재귀함수 -> 자기 자신을 부르는 것 -> 반드시 종료 조건이 필요

```py
# IT공학전공 2116313 손수경
# 1번을 해보세요!
def factorial(n):
    if n == 1:
        return 1
    else:
        return n * factorial(n - 1)


# 2번을 해보세요!
n = int(input())


# 출력합니다!
print(factorial(n))

```

## 실습 8

```py
# IT공학전공 2116313 손수경
# 1번을 해보세요!
def factorial(n):
    # None이라고 되어있는 부분을 수정해보세요
    result = 1
    for k in range(n, 0, -1):
        result = result * k
    return result


# 2번을 해보세요!
n = int(input())

# 출력합니다!
print(factorial(n))

```

## 실습 9

```py
# IT공학전공 2116313 손수경
# 1번을 해보세요!
n = int(input())

# 2번을 해보세요!


def hanoi_tower(n, fr, tmp, to):
    if(n == 1):
        print("원판 1: %s --> %s" % (fr, to))
    else:
        hanoi_tower(n - 1, fr, to, tmp)
        print("원판 %d: %s --> %s" % (n, fr, to))
        hanoi_tower(n - 1, tmp, fr, to)


# 출력합니다!
hanoi_tower(n, 'A', 'B', 'C')

```

## 실습 10

종료조건에서 n < 1일 때 return 0을 하나 위의 코드랑 똑같긴 함. 그렇다고 한 번 더 해서 비효율적인거는 아니다. 선택의 문제이다. <br>

기본연산은 묶을 수 있는 거는 하나로 묶는게 좋다. 진짜로 cpu에서는 사칙 연산 중 곱셈이 조금 더 느리긴하다. 덧셈도 실수 덧셈, 실수 곱셈, 정수 덧셈, 정수 곱셈 연산 속도는 다르지만 하나의 상수로 처리를 하는 것이다. <br>

덧셈기와 곱셈기가 따로 있고, 곱셈 전용 HW가 있다. 실제로는 CPU 클럭을 덧셈기는 한 번 쓰고, 곱셈기는 여러 번 쓴다. 기본적으로 실제적으로는 보는 것이 맞다. <br>

그러나 정해진 횟수만큼 도는 것이기 때문에 상수 하나로 봐도 된다.

```py
# IT공학전공 2116313 손수경
# 1번을 해보세요!
def binary_digits(n):
    if n <= 1:
        return 1
    else:
        return 1 + binary_digits(n // 2)


# 2번을 해보세요!
n = int(input())


# 출력합니다!
print(binary_digits(n))

```
