---
title: "[백준 2622번] 삼각형만들기"
excerpt: "[백준 2622번] 삼각형만들기"
categories: [Algorithm JavaScript]
tags: [Algorithm Study, JavaScript, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

```javascript
let input = require("fs").readFileSync("example.txt").toString();

let n = Number.parseInt(input);
let cnt = 0;
// maxLength >= midLength >= minLength
for (let minLength = 1; minLength <= n - minLength; minLength++) {
  for (
    let midLength = minLength;
    midLength <= n - minLength - midLength;
    midLength++
  ) {
    let maxLength = n - minLength - midLength;
    if (midLength + minLength > maxLength) cnt++;
  }
}
console.log(cnt);
```

## 풀이

min <= mid <= max의 크기를 갖고 있으므로 min부터 하나씩 설정하여서 2중 for문을 돌린다. n - min이라는 것은 n개에서 min개만큼 성냥개비를 사용했다는 것이고, n - min - mid라는 것은 n개에서 min과 mid개 만큼 성냥개비를 사용했다는 것이다.

- min = 1부터 n - min까지 돌리면서
- mid = min부터 n - min - mid까지 돌리면서
- max = n - min - mid : max를 구해서 삼각형 조건에 맞는지 확인한다.
