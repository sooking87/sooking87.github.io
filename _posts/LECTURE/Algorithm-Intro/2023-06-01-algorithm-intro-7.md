---
title: "Chap 06. 공간으로 시간벌기"
excerpt: "Chap 06. 공간으로 시간벌기"
categories: [Algorithm Intro]
tags: [Algorithm Intro, Python]
toc: true
toc_sticky: true
---

## 실습 1. 기수 정렬

```python
# 2116313 손수경
# 파이썬 queue모듈의 Queue 를 사용해요!
from queue import Queue


# 1번을 해보세요!
def radix_sort(A):
    queues = []
    for i in range(BUCKETS):
        queues.append(Queue())
    n = len(A)
    factor = 1
    for d in range(DIGITS):
        for i in range(n):
            queues[(A[i]//factor) % 10].put(A[i])
        j = 0
        for b in range(BUCKETS):
            while not queues[b].empty():
                A[j] = queues[b].get()
                j += 1
        factor *= 10
        print("step", d + 1, A)


# 2번을 해보세요!
data = [int(i) for i in input().split()]


# 출력합니다!
BUCKETS = 10		# 10진법으로 정렬
DIGITS = 4		# 최대 4 자릿수
radix_sort(data)						# 기수 정렬
print("Radix:", data)					# 결과 출력

```

## 실습 2. 카운팅 정렬

```python
# 2116313 손수경
# 1번을 해보세요!
def counting_sort(A):
    output = [0] * len(A)
    count = [0] * MAX_VAL

    for i in A:
        count[i] += 1
    for i in range(1, MAX_VAL):
        count[i] += count[i - 1]
    for i in range(len(A)):
        output[count[A[i]] - 1] = A[i]
        count[A[i]] -= 1
    for i in range(len(A)):
        A[i] = output[i]


# 2번을 해보세요!
data = [int(i) for i in input().split()]


# 출력합니다!
MAX_VAL = 10
print("Original  : ", data)
counting_sort(data)             # 카운팅 정렬
print("Counting  : ", data)

```

## 실습 3. 호스풀 알고리즘

```python
# 2116313 손수경
NO_OF_CHARS = 128

# 1번을 해보세요!


def shift_table(pat):
    m = len(pat)
    tbl = [m] * NO_OF_CHARS

    for i in range(m - 1):
        tbl[ord(pat[i])] = m - 1 - i
    return tbl


# 2번을 해보세요!
def search_horspool(T, P):
    m = len(P)
    n = len(T)
    t = shift_table(P)
    i = m - 1
    while i <= n - 1:
        k = 0
        while k <= m - 1 and P[m - 1 - k] == T[i - k]:
            k += 1
        if k == m:
            return i - m + 1
        else:
            i += t[ord(T[i])]
    return -1


# 3번을 해보세요!
text = input()
pattern = input()


# 출력합니다!
print("패턴의 위치 :", search_horspool(text, pattern))

```

## 실습 4. 선형 조사법의 삽입 알고리즘

```python
# 2116313 손수경
M = 13					# 테이블의 크기
table = [None]*M			# 테이블 만들기: None으로 초기화


def hashFn(key):		# 해시 함수
    return key % M

# 1번을 해보세요!


def lp_insert(key):
    id = hashFn(key)
    count = M
    while count > 0 and (table[id] != None):
        id = (id + 1 + M) % M
        count -= 1
    if count > 0:
        table[id] = key
    return


# 2번을 해보세요!
n = int(input())
for i in range(n):
    lp_insert(int(input()))

# 출력합니다!
print(table)

```

## 실습 5. 선형 조사법의 탐색 알고리즘

```python
# 2116313 손수경
M = 13					# 테이블의 크기


def hashFn(key):		# 해시 함수
    return key % M


# 1번을 해보세요!
def lp_search(key):
    id = hashFn(key)
    count = M
    while count > 0:
        if table[id] == None:
            return None
        if table[id] == key:
            return table[id]
        id = (id + 1 + M) % M
        count -= 1
    return None


# 2번을 해보세요!
table = [None if m == 'None' else int(m) for m in input().split()]
key = int(input())


# 출력합니다!
print(lp_search(key))

```

## 실습 6. 선형 조사법의 삭제 알고리즘

```python
# 2116313 손수경
M = 13					# 테이블의 크기


def hashFn(key):		# 해시 함수
    return key % M

# 1번을 해보세요!


def lp_delete(key):
    id = hashFn(int(key))
    count = M
    while count > 0:
        if table[id] == None:
            return
        if table[id] != -1 and table[id] == key:
            table[id] = -1
            return
        id = (id + 1 + M) % M
        count -= 1


# 2번을 해보세요!
table = [None if m == 'None' else int(m) for m in input().split()]
key = int(input())


# 출력합니다!
lp_delete(key)
print(table)

```

## 실습 7. 문자열 탐색키의 해시 함수 계산

```python
# 2116313 손수경
M = 13              # 테이블의 크기
table = [None]*M    # 테이블 만들기: None으로 초기화


# 1번을 해보세요!
def hashFn(key):
    sum = 0
    for c in key:
        sum = sum + ord(c)
    return sum % M


# 선형 조사법의 삽입 알고리즘
def lp_insert(key):
    id = hashFn(key)
    count = M
    while count > 0 and (table[id] != None and table[id] != -1):
        # while count>0 and (table[id] != None) :
        id = (id + 1 + M) % M
        count -= 1
    if count > 0:
        table[id] = key
    return


# 2번을 해보세요!
n = int(input())
for _ in range(n):
    lp_insert(input())


# 출력합니다!
print(table)

```
