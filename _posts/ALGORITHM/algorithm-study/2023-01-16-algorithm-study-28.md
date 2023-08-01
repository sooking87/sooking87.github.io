---
title: "[Python] 이분탐색(결정알고리즘) & 그리디 알고리즘"
excerpt: "이분탐색(결정알고리즘) & 그리디 알고리즘"
categories: [Algorithm Study]
tags: [Algorithm Study, Python, Algorithm]
toc: true
toc_sticky: true
---

## 이분 검색

이분 검색으로 한 거는 아님 ⏬

```python
n, m = map(int, input().split())
nums = list(map(int, input().split()))
nums.sort()
answer = 0

for i in range(len(nums)):
    if nums[i] == m:
        answer = (i + 1)
        break
print(answer)
```

### 이분 검색이란?

이분 검색이란 이진 탐색, 바이너리 서치라고도 불린다. <br>
BigO : `O(log N)` <br>
성능상으로 볼 떼, sort() 함수가 log N의 성능을 가진다. <br>

오름차순으로 정렬된 배열에서 원하는 숫자(target)을 찾는 알고리즘이다. <br>

1. 배열 전체의 중간값을 target과 비교
2. 중간값이 target 값보다 크면 왼쪽 부분만 비교
3. 왼쪽부터 중간값을 다시 target과 비교 <br>

<img width="1000" alt="download1" src="https://user-images.githubusercontent.com/96654391/212608916-36beded8-f5ba-4f8e-ba7f-b5bbc5c664ff.png"> <br>

이런 느낌? 무느알?

```python
n, m = map(int, input().split())
nums = list(map(int, input().split()))
nums.sort()
start = 0
end = n - 1

while start <= end:
    mid = (end + start) // 2
    if nums[mid] == m:
        print(mid + 1)
        break
    elif nums[mid] < m:
        start = mid + 1
    elif nums[mid] > m:
        end = mid - 1
```

## 랜선 자르기(결정알고리즘)

결정 알고리즘이란 위에 이분 검색을 활용하여 범위 내에서 특정 값을 찾아내는 문제이다. <br>

이 문제로 예를 들자면, n개의 개수만큼 랜선을 찾라야 되는데 자를 수 있는 랜선의 길이 중에서 최대값을 구하는 문제이다. <br>

```txt
4 11
802
743
457
539
```

답 범위가 1 ~ 802까지 가능은 하다. 일단 이렇게 범위를 잡는다. `(1 + 802) // 2` 로 했을 때, 그 길이가 최대로 잡을 수 있는 랜선 길이인지를 이분 검색을 통해서 확인을 한다. <br>
이 문제를 풀 때, 무조건 ==, >, < 식으로 조건을 나누는 것이 아니다. 왜냐하면 자를 수 있는 / 답의 개수만큼 자를 수 있는 값이 나와도 더 크게 자를 수 있다면 더 크게 잘라야 되므로 >=, <로 범위를 나누었다.

```python
def count(lenLine):
    cnt = 0
    for x in line:
        cnt += (x // lenLine)
    return cnt


k, n = map(int, input().split())
line = []
for _ in range(k):
    line.append(int(input()))

start = 1
end = max(line)
res = 0

while start <= end:
    mid = (start + end) // 2
    if count(mid) >= n:
        res = mid
        start = mid + 1
    elif count(mid) < n:
        end = mid - 1
print(res)
```

## 뮤직비디오(결정알고리즘)

연속적으로 m개의 DVD를 만드려고 하는데, 만들 수 있는 DVD의 최소 부른 곡의 길이가 몇인지를 구하는 문제이다. <br>

이 문제도 마찬가지로 이분 검색을 사용하는 문제인데, DVD개수가 m개보다 작거나 같으면 일단 답에 해당할 수 있다. 그러나 최소한의 DVD 개수를 구해야되는 것이므로 범위를 <=, > 로 쪼개어 준다. <br>
그리고 여기서 포인트는 count 함수가 될 것 같다. 왜냐하면 나는 인덱스를 기준으로 나누어야 되나? 라는 생각을 했었는데, 그게 아니라 인덱스 0부터 더해나가면서 이분 검색을 통해서 지정한 용량을 기준으로 크게 되면 DVD 개수를 늘리면서 sum을 다음 곡으로 초기화를 시켜준다. 이렇게 음악 리스트를 반복문을 돌리면서 해당 용량이 총 몇 개의 DVD를 필요로 하는지를 리턴해주는 것이다.

```python
def count(capacity):
    cnt = 1  # DVD 개수
    sum = 0
    for x in minute:
        if (sum + x) > capacity:
            cnt += 1
            sum = x
        else:
            sum += x
    return cnt


n, m = map(int, input().split())
minute = list(map(int, input().split()))
min = sum(minute)

maxx = max(minute)
start = 1
end = min
res = 0
while start <= end:
    mid = (start + end) // 2
    if mid >= maxx and count(mid) <= m:
        res = mid
        end = mid - 1
    else:
        start = mid + 1
print(res)
```

## 마구간 정하기(결정알고리즘)

```python
def count(distance):
    cnt = 1
    pos = room[0]
    for i in range(1, n):
        if room[i] - pos >= distance:
            cnt += 1
            pos = room[i]
    return cnt


n, c = map(int, input().split())
room = []
for _ in range(n):
    room.append(int(input()))
room.sort()

start = 1
end = max(room)
res = 0

while start <= end:
    mid = (start + end) // 2
    if count(mid) >= c:
        res = mid
        start = mid + 1
    else:
        end = mid - 1
print(res)
```

와,,, 진심 미쳤다. 왜냐면 <br>

1. 우선 결정 알고리즘이라는 카테고리를 보았고 지금까지 그렇게 풀었기 때문에 역시 이분 탐색을 사용해야될 것을 알았다. 하지만 start, end를 무엇으로 잡을지, 조건문은 어떻게 잡아야되는지 고민하는 것 조차 시간이 너무 오래걸렸다.
2. 고민을 하면서 start, end를 말들이 위치할 수 있는 위치의 시작과 끝점이라는 점, 탐색하는 것이 가리키는 것이 말들 사이의 거리라는 점은 알게 되었다. 하지만 조건문을 어떻게 활용할지를 몰랐다. 그니까 어떤 조건일 때 답이 되는 것이고 아닌 것인지를 알기가 어려웠다.
3. 잠깐 강의를 보고 힌트를 얻고 나서 말들을 기준으로 하는 것이라는 것을 알았고, c를 활용하기로 했다. <br>

하지만 count라는 함수를 나는 처음에 가능하다면 1씩 빼는 식으로 해서 음수거나 0보다 작거나 같으면 답으로 가능하다고 생각을 했다. 하지만 정확히 왜 안된지는 모르겠지만,,, 비슷한 루트로 하긴 함,,,,,,,,, 웨안뒈,,,,? <br>

그리고 애초에 나는 방의 위치가 있다면 1로 표시하고 아니라면 0으로 표시하는 리스트를 새로 만들었는데, 결국 방들 사이의 거리만 필요한 것이므로 입력받은 값들만 사용을 하면 되었다. <br>

여튼 결정 알고리즘이라는 테마를 기준으로 처음 문제 풀이를 해보았는데, 개념을 알고 있더라도 그 기준을 뭘로 잡을지 고민하는데 시간이 오래걸렸다. 많은 연습이 필요할 것 같다. <br>
보통 출력해야되는 값을 start, end, mid로 두는 것 같고, if, else 문에 조건문의 경우는 입력값을 기준으로 하는 것 같다,,

<small>일단 결정 알고리즘 마무리🌟</small>

<hr>

## 그리디 알고리즘

이 단계에서 가장 좋은 것을 선택하는 알고리즘 -> 정렬을 한 다음 선택을 해가면 된다.

## 회의실 배정(그리디)

```python
n = int(input())
# 회의가 끝나는 기준으로 정렬하면 됨
meeting = []
for _ in range(n):
    start, end = map(int, input().split())
    meeting.append((start, end))
# 회의가 끝나는 시간을 우선적으로 정렬 -> 그 다음 회의 시작 시간을 정렬
meeting.sort(key=lambda x: (x[1], x[0]))
endTime = 0
cnt = 0
for s, e in meeting:
    if s >= endTime:
        endTime = e
        cnt += 1
print(cnt)
```

sort() 함수를 사용할 때, 우선적으로 정렬을 해야되는 것을 결정할 때는 lambda를 사용해서 해주면 된다. <br>

그리디 알고리즘에서는 어떤 것을 기준으로 정렬을 해서 어떤 조건에 맞는 애들을 선택을 할 건지를 결정하는 것이 중요한 것 같다.

## 씨름 선수(그리디)

```python
n = int(input())
profile = []
for _ in range(n):
    height, weight = map(int, input().split())
    profile.append((height, weight))

profile.sort()
cnt = 0
for i in range(n):
    current = profile[i][1]
    canIn = True
    for j in range(i + 1, n):
        if current < profile[j][1]:
            canIn = False
    if canIn:
        cnt += 1

print(cnt)
```

정렬 기준을 키로 하고, 기준인 사람의 몸무게보다 뒤에 있는(정렬 기준 키큰 사람이) 모든 사람이 작으면 된다.

## 창고 정리(그리디)

가장 높은 열에서 가장 낮은 열로 n만큼 반복한다.

```python
l = int(input())
dummy = list(map(int, input().split()))
n = int(input())

for _ in range(n):
    highest = max(dummy)
    lowest = min(dummy)
    hIdx = dummy.index(highest)
    lIdx = dummy.index(lowest)
    dummy[hIdx] -= 1
    dummy[lIdx] += 1

print(max(dummy) - min(dummy))
```

그냥 dummy 리스트에서 큰 값과 작은 값의 인덱스를 찾아서 +/- 1을 하면 된다.

## 침몰하는 타이타닉(그리디)

```python
from collections import deque

n, m = map(int, input().split())
weight = list(map(int, input().split()))

weight.sort()
weight = deque(weight)
cnt = 0
temp = 0
while weight:
    if len(weight) == 1:
        cnt += 1
        break
    if weight[0] + weight[-1] > m:
        weight.pop()
        cnt += 1
    else:
        weight.popleft()
        weight.pop()
        cnt += 1

print(cnt)
```

- 앞뒤로 제거가 필요하다 -> deque 활용
- pop, popleft를 해서 리스트의 길이가 달라져서 for문을 사용할 수 없다 -> while을 사용해서 안에 값이 있을동안 반복문을 돌린다.

## 증가 수열 만들기(그리디)

```python
from collections import deque

n = int(input())
nums = list(map(int, input().split()))
nums = deque(nums)
cnt = 0
res = ""
delNum = 0
while nums:
    if delNum < min(nums[0], nums[-1]):
        if nums[0] > nums[-1]:
            res += "R"
            delNum = nums.pop()
        else:
            res += "L"
            delNum = nums.popleft()
    else:
        if max(nums[0], nums[-1]) == nums[0]:
            res += "L"
            delNum = nums.popleft()
        else:
            res += "R"
            delNum = nums.pop()
    cnt += 1

    if (delNum > nums[0]) and (delNum > nums[-1]):
        break
print(cnt)
print(res)
```

살짝 비효율적이긴 한데,,,,,,,,, 그래도 처음부터 이렇게 풀고 싶었으니까 꾸역꾸역 품,,

## 역수열(그리디)

```python
n = int(input())
reverse = list(map(int, input().split()))
res = [0 for i in range(n)]
for i in range(n):
    for j in range(n):
        if (reverse[i] == 0 and res[j] == 0):
            res[j] = i + 1
            break
        elif res[j] == 0:
            reverse[i] -= 1
for x in res:
    print(x, end=' ')
```

n개의 0을 리스트로 만들어서 그 리스트가 0인 자리를 카운트하면서 0인 자리에 해당 숫자를 넣는다. <br>
여기서 카운트를 하는 방법은 res에서 0을 찾을 때마다 1씩 역순열을 줄여나가면 된다.
