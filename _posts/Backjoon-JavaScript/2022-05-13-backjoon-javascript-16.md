---
title: "[백준 1978번] 소수 찾기"
excerpt: "[백준 1978번] 소수 찾기"
categories: [Backjoon JavaScript]
tags: [Backjoon, JavaScript]
toc: true
toc_sticky: true
---

```js
let input = require("fs").readFileSync("example.txt").toString().split("\n");

var n = parseInt(input.shift());

// 두 번째 입력값을 가져와서(shift), 쪼개고(split), 정수형으로 바꾸어줌
var a = input
  .shift()
  .split(" ")
  .map((x) => parseInt(x));

var cnt = 0;
a.forEach((x) => {
  var isPrimeNum = true;
  if (x === 1) isPrimeNum = false;
  if (x === 2 || x === 3) {
    cnt++;
  } else {
    for (var i = 2; i <= Math.floor(Math.sqrt(x)); i++) {
      if (x % i === 0) {
        isPrimeNum = false;
      }
    }
    if (isPrimeNum === true) cnt++;
  }
});

console.log(cnt);
```

## 풀이

1. 소수인지 아닌지 판별하기 위해서는 그 수의 루트값만큼까지 나누어봐서 0인지 아닌지 판별하면 됨
2. 1은 소수가 아님을 빼먹지 말 것
