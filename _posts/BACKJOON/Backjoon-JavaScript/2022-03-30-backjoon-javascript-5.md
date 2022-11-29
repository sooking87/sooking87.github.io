---
title: "[백준 1145번] 적어도 대부분의 배수"
excerpt: "[백준 1145번] 적어도 대부분의 배수"
categories: [Backjoon JavaScript]
tags: [Backjoon, JavaScript]
toc: true
toc_sticky: true
---

```javascript
let input = require("fs").readFileSync("example.txt").toString().split(" ");
let nums = [];
let min = 100;
for (let i = 0; i < input.length; i++) {
  nums[i] = parseInt(input[i]);
  if (min > nums[i]) {
    min = nums[i];
  }
}

while (true) {
  let cnt = 0;
  for (let i = 0; i < nums.length; i++) {
    if (min % nums[i] === 0) {
      cnt++;
    }
  }
  if (cnt >= 3) {
    break;
  }
  min++;
}
console.log(min);
```

## 문제 풀이

입력된 수는 100을 넘지 않는다고 하였으므로 최소를 100으로 두고 최솟값을 잡는다. 그런다음 최솟값부터 1씩 늘려가면서 나누어 떨어지는 값이 3개 이상이 될때까지 반복문을 돌린다.
