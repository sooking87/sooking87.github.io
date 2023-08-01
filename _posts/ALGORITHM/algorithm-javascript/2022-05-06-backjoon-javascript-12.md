---
title: "[백준 1924번] 2007년"
excerpt: "[백준 1924번] 2007년"
categories: [Algorithm JavaScript]
tags: [Algorithm Study, JavaScript, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

```javascript
let input = require("fs").readFileSync("example.txt").toString().split(" ");
let month = Number.parseInt(input[0]);
let day = Number.parseInt(input[1]);
let days = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31];
let week = ["SUN", "MON", "TUE", "WED", "THU", "FRI", "SAT"];
let cnt = 0;

// 인덱스상 month - 1이 실제 month임
for (let i = 0; i < month - 1; i++) {
  cnt += days[i];
}

for (let i = 1; i <= day; i++) {
  cnt++;
}

console.log(week[cnt % 7]);
```

## 풀이

1월 1일이 월요일이기에 일수를 더한 후 7로 나눈 나머지가 요일이라고 할 수 있다.
