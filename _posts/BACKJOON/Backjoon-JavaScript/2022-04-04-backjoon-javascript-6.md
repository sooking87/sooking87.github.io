---
title: "[백준 2839번] 설탕 배달"
excerpt: "[백준 2839번] 설탕 배달"
categories: [Backjoon JavaScript]
tags: [Backjoon, JavaScript]
toc: true
toc_sticky: true
---

```javascript
let input = require("fs").readFileSync("example.txt").toString();
let n = parseInt(input);
let cnt = 0;
while (true) {
  //봉지의 최소 개수를 구할려면 5로 나눈 몫을 구하는게 좋음
  if (n % 5 == 0) {
    cnt += n / 5;
    n = 0;
  }
  if (n <= 0) {
    break;
  }
  //근데 만약에 5로 안나누어 떨어지면 일단 3 키로 봉지에 하나 담고 다시 5로 나누어 떨어지는지 확인
  n -= 3;
  cnt++;
}
//n이 음수이면 봉지로 나누어 담을 수 없음.
console.log(n < 0 ? -1 : cnt);
```

## 풀이

넘 많이 풀어서,,,걍 외움
