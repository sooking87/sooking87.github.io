---
title: "[백준 1890][DynamicProgramming1] 점프"
excerpt: "[백준 1890][DynamicProgramming1] 점프"
categories: [Algorithm Python]
tags: [Algorithm Study, Python, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

📌 [백준 1890 문제 링크](https://www.acmicpc.net/problem/1890) <br>

## 백준 1890 점프

N×N 게임판: 0은 종착점, 항상 현재 칸에 적혀있는 수만큼 오른쪽이나 아래로 가야된다. -> (0, 0) 위치에서 규칙에 맞게 이동할 수 있는 경로의 개수

## 대충 코드

```python
# 1890 점프

# N×N 게임판: 0은 종착점, 항상 현재 칸에 적혀있는 수만큼 오른쪽이나 아래로 가야된다. -> (0, 0) 위치에서 규칙에 맞게 이동할 수 있는 경로의 개수

import sys


def row_first(cnt, col, row):
    # print(cnt, col, row)
    if col == n - 1 and row == n - 1:
        print("끝", cnt)
        cnt[col][row] += 1

        print(cnt, col, row)
        ans = cnt[col][row]
        return ans
    temp_row = row + board[col][row]
    temp_col = col + board[col][row]
    if temp_row >= 0 and temp_row < n:  # 오른쪽으로 이동 = 열 이동
        cnt[col][board[col][row]] += 1
        row += board[col][row]
        print('오른쪽으로 이동', cnt, col, row)
        return row_first(cnt, col, row)
    if temp_col >= 0 and temp_col < n:  # 아래로 이동 = 행 이동
        cnt[board[col][row]][row] += 1
        col += board[col][row]
        print('아래쪽으로 이동', cnt, col, row)
        return row_first(cnt, col, row)


def col_first(cnt, col, row):
    # print(cnt, col, row)
    if col == n - 1 and row == n - 1:
        print("끝", cnt)
        cnt[col][row] += 1

        print(cnt, col, row)
        ans = cnt[col][row]
        return ans
    temp_row = row + board[col][row]
    temp_col = col + board[col][row]

    if temp_col >= 0 and temp_col < n:  # 아래로 이동 = 행 이동
        cnt[board[col][row]][row] += 1
        col += board[col][row]
        print('아래쪽으로 이동', cnt, col, row)
        return col_first(cnt, col, row)
    if temp_row >= 0 and temp_row < n:  # 오른쪽으로 이동 = 열 이동
        cnt[col][board[col][row]] += 1
        row += board[col][row]
        print('오른쪽으로 이동', cnt, col, row)
        return col_first(cnt, col, row)


input = sys.stdin.readline
n = int(input())
board = [[int(i) for i in input().split()] for _ in range(n)]
cnt = [[0 for i in range(n)] for _ in range(n)]
col = 0
row = 0
result = 0
result += row_first(cnt, col, row)
result += col_first(cnt, col, row)
print("결과 도출:", result)
```

뭐 나름.. 메모이제이션을 공부를 해보고 cnt에서 간 데를 1씩 늘리면서 최종 (n, n)위치의 값을 출력하고자 함. <br>

근데 오른쪽으로 가는 방법과 아래쪽으로 가는 방법 두 가지가 있는데, 그걸 어케 해야될지 모르겠음. -> 제일 깊이 까지 내려갔다가 올라오는 식.. 이런거 했는데 무슨 문제였더라.

## 풀이 코드

```python
# 1890 점프

# N×N 게임판: 0은 종착점, 항상 현재 칸에 적혀있는 수만큼 오른쪽이나 아래로 가야된다. -> (0, 0) 위치에서 규칙에 맞게 이동할 수 있는 경로의 개수

import sys

input = sys.stdin.readline
n = int(input())
board = [[int(i) for i in input().split()] for _ in range(n)]
cnt = [[0 for i in range(n)] for _ in range(n)]
cnt[0][0] = 1  # 초기 값

for col in range(n):
    for row in range(n):
        if col == n - 1 and row == n - 1:
            print(cnt[col][row])
            break
        # 오른쪽으로 이동
        if row + board[col][row] < n:
            cnt[col][row + board[col][row]] += cnt[col][row]

        # 아래쪽으로 이동
        if col + board[col][row] < n:
            cnt[col + board[col][row]][row] += cnt[col][row]
        # print(cnt, cnt[col][row], col, row)
```

아 생각했던거랑 비슷한데! 이중포문은 몰랐네,, 직접 하나하나 보면서 얘가 board 내에서 이동이 가능한지 아닌지만 보면 됐다. <br>

하지만 궁금한거는 왜 `cnt[col][row]` 만큼을 왜 더하는지 모르겠다. 1을 더하는 게 아니라,,, -> 현재까지 간 횟수만큼 다음 이동 칸으로 갈 수 있다.

## 코드 설명

규칙이 있었고, 2중 포문을 돌리면서 가능한 모든 경우의 수를 cnt에 하나씩 추가해나아갔다. <br>

여기서 이중 반복문의 DP를 알 수 있다.
