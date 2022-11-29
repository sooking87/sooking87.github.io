---
title: "[백준 11021번] A + B - 7"
excerpt: "[백준 11021번] A + B - 7"
categories: [Backjoon JavaScript]
tags: [Backjoon, JavaScript]
toc: true
toc_sticky: true
---

```javascript
let input = require("fs").readFileSync("example.txt").toString().split("\n");
let n = parseInt(input[0]);
for (let i = 1; i <= n; i++) {
  let nums = input[i].split(" ");

  console.log(`Case #${i}: ${Number(nums[0]) + Number(nums[1])}`);
}
```

## 풀이

백준에서 백틱으로 푸는 것을 요구했던 것 같다. 처음에 "Case #" + i + ": ", sum이런 식으로 했는데 계속 출력형식이 잘못되었다고 나옴. Number는 자바 스크립트에서 숫자형을 말하는 것!

- 선언할 수 있는 타입
  - let
  - const
  - var
- 원시 값 / 데이터형(선언할 수는 없음) : 불변 값
  - Number
  - String
  - Boolean
  - Null
  - Undefined
  - BigInt
  - Symbol
