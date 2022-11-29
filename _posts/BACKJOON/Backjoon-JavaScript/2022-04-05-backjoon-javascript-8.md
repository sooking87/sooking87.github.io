---
title: "[백준 2869번] 달팽이는 올라가고 싶다."
excerpt: "[백준 2869번] 달팽이는 올라가고 싶다."
categories: [Backjoon JavaScript]
tags: [Backjoon, JavaScript]
toc: true
toc_sticky: true
---

❌ 시간 초과 ❌

```javascript
let input = require("fs").readFileSync("example.txt").toString().split(" ");
let a = Number.parseInt(input[0]);
let b = Number.parseInt(input[1]);
let v = Number.parseInt(input[2]);
let dayCount = 0;
let upDown = 0;
while (true) {
  dayCount++;
  upDown += a;
  if (upDown >= v) {
    break;
  }
  upDown -= b;
}
console.log(dayCount);
```

💥 이마 탁

```javascript
let input = require("fs").readFileSync("example.txt").toString().split(" ");
let a = Number.parseInt(input[0]);
let b = Number.parseInt(input[1]);
let v = Number.parseInt(input[2]);

console.log(Math.ceil((v - b) / (a - b)));
```

## 풀이

a만큼 정상에 올라가면 stop이므로 일단 내려올 만큼 빼주고 a - b를 나누고, 마지막날 하루 올라간 만큼을 더해주기 위해서 올림을 사용.
(높이에서 밤에 미끄러지는 높이)인 높이까지만 올라가면 다음날 정상에 도착 가능(Math.ceil)
