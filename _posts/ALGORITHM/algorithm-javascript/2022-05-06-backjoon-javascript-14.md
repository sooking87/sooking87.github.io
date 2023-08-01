---
title: "[백준 1018번] 체스판 다시 칠하기"
excerpt: "[백준 1018번] 체스판 다시 칠하기"
categories: [Algorithm JavaScript]
tags: [Algorithm Study, JavaScript, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

```javascript
const fs = require("fs");
let input = fs.readFileSync("example.txt").toString().split("\n");

// 정상 보드판
let white = [
  "WBWBWBWB",
  "BWBWBWBW",
  "WBWBWBWB",
  "BWBWBWBW",
  "WBWBWBWB",
  "BWBWBWBW",
  "WBWBWBWB",
  "BWBWBWBW",
];
let black = [
  "BWBWBWBW",
  "WBWBWBWB",
  "BWBWBWBW",
  "WBWBWBWB",
  "BWBWBWBW",
  "WBWBWBWB",
  "BWBWBWBW",
  "WBWBWBWB",
];

[size, ...board] = input;
[n, m] = size.split(" "); // n = 행, m = 열
board = board.map((line) => line.trim().split(""));
let answer = 90;

for (let i = 0; i <= n - 8; i++) {
  for (let j = 0; j <= m - 8; j++) {
    check(i, j);
  }
}

function check(x, y) {
  let checkWhite = 0; //흰색을 수정해야 되는 개수
  let checkBlack = 0; //검은색을 수정해야 되는 개수

  //0,0부터 m-8,n-8까지 검색
  for (let i = x; i < x + 8; i++) {
    for (let j = y; j < y + 8; j++) {
      if (board[i][j] !== white[i - x][j - y]) checkWhite++;
      if (board[i][j] !== black[i - x][j - y]) checkBlack++;
    }
  }

  let min = checkBlack < checkWhite ? checkBlack : checkWhite;

  if (min < answer)
    //answer보다 min이 작은 경우 answer를 최솟값으로 초기화
    answer = min;
}
console.log(answer);
```

## 풀이

- 처음에 있는 이중 포문 : 검사를 해야되는 시작행, 시작열

- check() 함수 : 검정색이 변했을 때가 최소인지, 흰색이 변했을 때가 최소인지를 판단 그리고 그 최소가 기존의 answer보다 작으면 answer에 대입

- check() 함수의 반복문 범위를 보면 시작행, 시작열 기준으로 딱 8번씩 반복한다. 8\*8 보드판이기 때문이다.

## 배운 점

```javascript
[size, ...board] = input;
[n, m] = size.split(" "); // n = 행, m = 열
board = board.map((line) => line.trim().split(""));
```

이런 식으로 입력 받아진 값들을 처리할 수 있다는 점!
