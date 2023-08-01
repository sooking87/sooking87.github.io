---
title: "[백준 2562번] 최댓값"
excerpt: "[백준 2562번] 최댓값"
categories: [Algorithm JavaScript]
tags: [Algorithm Study, JavaScript, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

```javascript
let input = require("fs").readFileSync("example.txt").toString().split("\n");

let max = Number.parseInt(input[0]);
let index = 0;

for (let i = 1; i < 9; i++) {
  if (max < input[i]) {
    index = i;
    max = input[i];
  }
}

console.log(max);
console.log(index + 1);
```

## 풀이

최댓값, 그에 해당하는 숫자가 몇 번째에 있는지 출력하는 문제! 몇 번째인 경우는 인덱스 + 1임을 명심 ❗
