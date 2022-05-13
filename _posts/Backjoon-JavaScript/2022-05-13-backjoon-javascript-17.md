---
title: "[백준 1085번] 직사각형에서 탈출"
excerpt: "[백준 1085번] 직사각형에서 탈출"
categories: [Backjoon JavaScript]
tags: [Backjoon, JavaScript]
toc: true
toc_sticky: true
---

```js
let input = require("fs").readFileSync("example.txt").toString().split(" ");

var arr = input.map((x) => parseInt(x));

var a = Math.abs(arr[0] - arr[2]);
var b = Math.abs(arr[0] - 0);
var c = Math.abs(arr[1] - arr[3]);
var d = Math.abs(arr[1] - 0);

var result = Math.min(a, b, c, d);
console.log(result);
```

## 풀이

- JS : Math.min([숫자 집합]) → 숫자 집합 중 가장 작은 값을 리턴
- Java : Math.min(a, b) → 두 수를 비교해서 작은 값을 리턴
