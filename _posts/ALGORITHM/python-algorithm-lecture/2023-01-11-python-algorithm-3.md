---
title: "[Python] 섹션 3. 탐색&시뮬레이션(string, 1차원, 2차원 리스트 탐색 )"
excerpt: "섹션 3. 탐색&시뮬레이션(string, 1차원, 2차원 리스트 탐색 )"
categories: [Python Algorithm]
tags: [Python Algorithm, Python, Algorithm]
toc: true
toc_sticky: true
---

## 회문 문자열 검사

```python
n = int(input())

for i in range(n):
    word = input()
    word = word.lower()
    lenWord = len(word) - 1
    isSame = True
    for j in range(lenWord):
        if word[j] != word[len(word) - 1 - j]:
            isSame = False

    if isSame:
        print("#%d YES" % (i + 1))
    else:
        print("#%d NO" % (i + 1))
```

## 숫자만 추출

```python
def getDivisor(num):
    divisorList = []
    for i in range(1, num + 1):
        if num % i == 0:
            divisorList.append(i)
    return divisorList


t = input()
answer = ""
for i in range(len(t)):
    if t[i] >= '0' and t[i] <= '9':
        answer += t[i]

answer = int(answer)
print(answer)
print(len(getDivisor(answer)))
```

## 카드 역배치

```python
def getReverse(switchCards):
    temp = []
    for i in range(len(switchCards)-1, -1, -1):
        temp.append(switchCards[i])
    return temp


cards = [i for i in range(1, 21)]

for i in range(10):
    a, b = map(int, input().split())
    switchCards = cards[a - 1: b]
    switchCards = getReverse(switchCards)
    cards[a - 1: b] = switchCards

for i in cards:
    print(i, end=' ')
```

시간이 조금 걸렸던 이유 <br>

1. 리스트를 슬라이스를 통해서 일부만 sort를 할 수 없다.
2. sort(reverse=True)를 사용하는게 아니라 진짜 말 그래도 순서를 역으로 바꾸는 것이었다.

## 두 리스트 합치기

```python
n1 = int(input())
firstList = list(map(int, input().split()))
n2 = int(input())
secondList = list(map(int, input().split()))

answer = firstList + secondList
answer.sort()

for i in answer:
    print(i, end=' ')
```

이거는 무슨 문젤까,,,, ㅎㅎㅎㅎ 리스트 더하고 sort 하면 됨

## 수들의 합

## 격자판 최대합

```python
n = int(input())
board = []

for i in range(n):
    row = list(map(int, input().split()))
    board.append(row)

sum = []
for row in range(n):
    temp1 = 0
    temp2 = 0
    for col in range(n):
        temp1 += board[row][col]
        temp2 += board[col][row]
    sum.append(temp1)
    sum.append(temp2)

temp = 0
for i in range(n):
    temp += board[i][i]
sum.append(temp)

print(max(sum))
```

그냥 격자판에서 가능한 합은 모두 구한 후 거기서 최대값을 구한다.

## 사과나무(다이아몬드)

```python
n = int(input())
farm = []
for i in range(n):
    temp = list(map(int, input().split()))
    farm.append(temp)

start = n // 2
end = start + 1
sum = 0
for row in range((n // 2) + 1):
    for col in range(start, end):
        sum += farm[row][col]
    start -= 1
    end += 1

start += 1
end -= 1
for row in range((n // 2) + 1, n):
    start += 1
    end -= 1
    for col in range(start, end):
        sum += farm[row][col]

print(sum)
```

약간 다이아몬드 점찍기처럼 인덱스를 필요로 하고 있다. <br>
이 문제는 좌표에서 다이아몬드 모양으로 그 안에 있는 숫자의 합을 구한다.

## 곶감(모래시계)

0이면 왼쪽으로 1이면 오른쪽으로 첫 번째 입력값에 해당하는 행에 마지막 입력값만큼 이동으로 시키고 모래시계 모양으로 합을 구하는 문제이다.

```python
def getMoved(n, arrow, space, list):
    moved = []
    if arrow == 0:
        for i in range(len(list)):
            moved.append(list[(i + space) % n])
    if arrow == 1:
        haveToMove = n - space
        for i in range(len(list)):
            moved.append(list[(i + haveToMove) % n])
    return moved


def getSum(ground):
    n = len(ground)
    start = 0
    end = n
    sum = 0
    for row in range((n // 2) + 1):
        for col in range(start, end):
            sum += ground[row][col]
        start += 1
        end -= 1
    start -= 1
    end += 1
    for row in range((n // 2) + 1, n):
        start -= 1
        end += 1
        for col in range(start, end):
            sum += ground[row][col]
    return sum

# 0이면 왼쪽, 1이면 오른쪽
n = int(input())
ground = []
for i in range(n):
    temp = list(map(int, input().split()))
    ground.append(temp)

commandCnt = int(input())
for i in range(commandCnt):
    row, arrow, space = map(int, input().split())
    copy = ground[row - 1]
    movedList = getMoved(n, arrow, space, copy)
    ground[row - 1] = movedList

sum = getSum(ground)
print(sum)
```

## 봉우리

## 스토쿠 검사

## 격자판 회문수
