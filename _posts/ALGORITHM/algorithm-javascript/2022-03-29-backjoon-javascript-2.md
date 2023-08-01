---
title: "[백준 2588번] 곱셈"
excerpt: "[백준 2588번] 곱셈"
categories: [Algorithm JavaScript]
tags: [Algorithm Study, JavaScript, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

```javascript
let input = require("fs").readFileSync("/dev/stdin").toString().split("\n");

let num1 = parseInt(input[0]);
let num2 = input[1]; //문자열
let sum = 0;

for (let i = num2.length - 1; i >= 0; i--) {
  let temp = num1 * parseInt(num2.charAt(i));
  console.log(temp);
}
console.log(num1 * num2);
//num2 -> 굳이 문자열을 숫자열로 바꿔줄 필요 X
```

## 문제 풀이

sol 1의 경우는 하나씩 곱해진 값을 가지고 Math.pow를 이용해서 자리수를 맞춰주었지만, 이런 과정 없이 그냥 num1 \* num2를 하여서 마지막 출력값을 출력합니다.
