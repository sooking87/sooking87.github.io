---
title: "[Python] 코드 구현력 기르기"
excerpt: "코드 구현력 기르기"
categories: [Python Algorithm]
tags: [Python Algorithm, Python, Algorithm]
toc: true
toc_sticky: true
---

## 1. K번째 약수 풀이

```python
# N의 약수 중 K번째로 작은 수 출력

N, K = map(int, input().split())
'''
nums = []
for i in range(1, N + 1):
    if (N % i == 0):
        nums.append(i)

if (len(nums) <= K):
    print(-1)
else:
    print(nums[K - 1])
'''

cnt = 0
for i in range(1, N + 1):
    if N % i == 0:
        cnt += 1
    if cnt == K:
        print(i)
        break
# for 문이 정상 완료가 된다면 else 문 실행
else:
    print(-1)
```

for-else 문이 있는데 for문이 정상종료되면 else문이 들어가게 된다. 여기서 for문이 정상 종료가 되었다는 것은 K번 째에 해당하는 숫자가 없다는 뜻이므로 -1을 출력

## 2. K번째 수

```python
t = int(input())
for i in range(t):
    n, s, e, k = map(int, input().split())
    nums = list(map(int, input().split()))
    temp = nums[s - 1: e]
    temp.sort()
    print("#%d %d" % (i + 1, temp[k - 1]))
```

## 3. K번째 큰 수

삼중포문 안쓰고 어떻게 구현할 수 있나 강의를 봤는데 역시 삼중포문 사용.

```python
n, k = map(int, input().split())
nums = list(map(int, input().split()))
res = set()  # 이렇게 set을 해두면 res에 어떤 숫자든 한개만 들어가게 된다. 중복 제거
for i in range(n):
    for j in range(i + 1, n):
        for m in range(j + 1, n):
            res.add(nums[i] + nums[j] + nums[m])

res = list(res)
res.sort(reverse=True)  # 내림차순
print(res[k - 1])
```

1. `res = set()` 을 하게 되면 res에 넣는 숫자들은 중복이 제거된다. set에 값을 추가하려면 add를 사용한다.
2. `res.sort(reverse = True)` : 내림차순 정렬

## [선수지식]최솟값 구하기

## 대표값

평균을 첫째자리에서 올림을 하고(round) 평균과 가장 가까운 인덱스 번호를 구하는 문제. 만약에 평균과 가까운 점수가 여러명이라면 점수가 더 큰 인덱스 중 작은 인덱스를 출력

```python
n = int(input())
scores = list(map(int, input().split()))
sum = 0

for i in range(n):
    sum += scores[i]

avg = round(sum / n)

minDiff = 100
minNum = 0
for i in range(len(scores)):
    temp = abs(avg - scores[i])
    if (temp < minDiff):
        minDiff = temp
        score = scores[i]
        minNum = i + 1
    elif (temp == minDiff):
        if (score < scores[i]):
            score = scores[i]
            minNum = i + 1

print(avg, minNum)
```

평균과 점수 차이가 적은 점수(score)을 따로 변수로 만든 이유는 점수 차이가 같은 점수들 중 큰 점수를 구하려고 한 것이다. <br>

파이썬에서 round 함수는 round_half_even 방식을 사용해서 even(0.500)으로 딱 떨어지면 버림을 해버린다. 하지만 우리가 예상하던 round 함수는 사사오입이기 때문에 다음과 같이 수정한다.

```python
avg = sum / n
avg += 0.5
avg = int(avg)
```

0.5를 더하고 int 형으로 바꾸어 소수점을 버리면 소수점이 5부터는 올림을 해주고 4까지는 버림이 된다.

## 정다면체

문제가 조금 어렵게 나와있긴 한데, 정 n면체와 정 m면체가 주어지면 1부터 n과 1부터 m까지의 나올 수 있는 모든 합 중 가장 많이 나오는 합의 값을 구하라는 문제이다.

```python
n, m = map(int, input().split())
res = [0 for i in range(n + m + 1)]

for i in range(1, n + 1):
    for j in range(1, m + 1):
        temp = i + j
        res[temp] += 1

max = 0
for i in range(len(res)):
    if (max < res[i]):
        max = res[i]

for i in range(len(res)):
    if (max == res[i]):
        print(i, end=' ')
```

## 자릿수의 합

```python
n = int(input())
nums = list(map(int, input().split()))

maxSum = 0
maxIdx = 0
for i in range(len(nums)):
    sum = 0
    for j in range(len(str(nums[i]))):
        sum += int(str(nums[i])[j])

    if (sum > maxSum):
        maxSum = sum
        maxIdx = i
print(nums[maxIdx])
```

/ 가 안되서 일단은 숫자를 문자열로 바꾸어서 인덱스를 통해서 숫자를 하나씩 접근하긴 했다. 하지만 철쁠때도 많이 들었던 것 처럼 숫자를 10으로 나눈 나머지를 더하고, 10으로 나누어서 그 다음 자릿수의 합을 구하는 것을 배웠다. 이 경우는 다음과 같이 구현할 수 있다.

```python
def digit_sum(x):
    sum = 0
    while x > 0:
        sum += x % 10
        x = x // 10
    return sum


n = int(input())
nums = list(map(int, input().split()))
res = 0
max = 0
for i in nums:
    temp = digit_sum(i)
    if (temp > max):
        max = temp
        res = i
print(res)
```

파이썬에서는 %가 나머지 구하는 연산, //가 몫을 구하는 연산이다.

## 소수(에라토스테네스 체)

1부터 N까지의 숫자 중에서 소수를 찾는다고 할 때, 우선 N만큼 리스트를 0으로 초기화를 시켜둔다. <br>
그런 다음 인덱스 2부터 반복분을 돌리면서 0이면 소수로 판별을 하고 카운트 1을 해준다. 그 다음 리스트 내에서의 2의 배수를 모두 1로 바꾼다.

```python
# 소수 개수 구하기(에라토스테네스 체)

n = int(input())
cnt = [0] * (n + 1)
res = 0

for i in range(2, n + 1):
    if (cnt[i] == 0):
        res += 1
        for j in range(i, n + 1, i):
            if j % i == 0:
                cnt[j] = 1
print(res)
```

소수를 구하는 방법 중에서 가장 빠른 방법이라고 한다.

## 뒤집은 소수

```python
def reverse(x):
    num = 0
    k = 1
    for i in range(len(str(x))):
        num += k * int(str(x)[i])
        k *= 10
    return num


def isPrime(x):
    if x == 1:
        return False
    for i in range(2, x):
        if x % i == 0:
            return False
    else:
        return True


n = int(input())
nums = list(map(int, input().split()))
for i in nums:
    revNum = reverse(i)
    if (isPrime(revNum)):
        print(revNum, end=' ')
```

## 주사위 게임

```python
n = int(input())
money = []

for i in range(n):
    tempMoney = 0
    dice = list(map(int, input().split()))
    dice.sort()
    setDice = set(dice)
    lenSet = len(setDice)
    if (lenSet == 1):
        tempMoney = 10000 + dice[0] * 1000
    elif (lenSet == 2):
        tempMoney = 1000
        # 같은 눈 2개인 경우 같은 눈 찾기
        if (dice[0] == dice[1]):
            tempMoney += dice[0] * 100
        else:
            tempMoney += dice[2] * 100
    else:
        tempMoney = dice[2] * 100
    money.append(tempMoney)

money.sort()
print(money[n - 1])
```

## 점수계산

정답이 연속되면 연속된 개수만큼 점수가 더해지는 문제. 111이면 1 + 2 + 3으로 진행된다.

```python
n = int(input())
ox = list(map(int, input().split()))
score = 0
isContinue = 1

for i in ox:
    if (i == 1) and (isContinue >= 1):
        score += isContinue
        isContinue += 1
    elif (i == 0):
        isContinue = 1
        continue
print(score)
```

<br>
정답 코드 ⏬

```python
n = int(input())
score = list(map(int, input().split()))
cnt = 0  # 연속되어서 맞추었는지 아닌지 확인
sum = 0
for i in range(n):
    if (score[i] == 1):
        cnt += 1
        sum += cnt
    else:
        cnt = 0

print(sum)
```

굳이 isContine가 1보다 큰지 작은지 판별할 필요가 없었다고 한다,,,,,
