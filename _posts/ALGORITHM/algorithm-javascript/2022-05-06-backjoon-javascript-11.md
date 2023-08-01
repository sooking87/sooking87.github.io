---
title: "[백준 4641번] Doubles"
excerpt: "[백준 4641번] Doubles"
categories: [Algorithm JavaScript]
tags: [Algorithm Study, JavaScript, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

```javascript
let input = require("fs").readFileSync("example.txt").toString().split("\n");

let i = 0;

while (true) {
  let temp = input[i];
  let cnt = 0;

  if (temp === "-1") {
    break;
  }
  let arr = input[i].trim().split(" "); // 배열

  // arr.length - 1 -> 0은 제외해야되니까
  arr.forEach((standard) => {
    arr.forEach((compare) => {
      if (Number.parseInt(standard) * 2 === Number.parseInt(compare)) {
        cnt++;
      }
    });
  });
  console.log(cnt - 1);
  i++;
}
```

## 풀이

arr.forEach 배열 내장함수 활용
