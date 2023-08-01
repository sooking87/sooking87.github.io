---
title: "[백준 2740번] 행렬 곱셈"
excerpt: "[백준 2740번] 행렬 곱셈"
categories: [Algorithm JavaScript]
tags: [Algorithm Study, JavaScript, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

```js
let input = require("fs").readFileSync("example.txt").toString().split("\n");
let input2 = input.map((elm) => elm.split(" ").map((x) => parseInt(x)));

// 배열 a 행 / 렬
const a = [];
const b = [];

// a배열 만들기
var [aN, aM] = input2.shift();
for (var i = 0; i < aN; i++) {
  a.push(input2.shift());
}

// b배열 만들기
var [bN, bM] = input2.shift();
for (var i = 0; i < bN; i++) {
  b.push(input2.shift());
}

// b배열의 행과 열 위치 바꾸기
var c = [];
while (b[0].length > 0) {
  var temp = [];
  // b의 행만큼 반복문을 돌면서 앞에서부터 하나씩 빼서 temp에 넣어주기
  for (var i = 0; i < bN; i++) {
    temp.push(b[i].shift());
  }
  c.push(temp);
}

const result = [];
// aN * bM 배열이 된다.
for (var i = 0; i < aN; i++) {
  var temp = [];
  var row = a[i]; // i번째 행 기준으로 c 배열의 j행들을 처리

  for (var j = 0; j < bM; j++) {
    var sum = 0;
    var col = c[j];
    for (var k = 0; k < aM; k++) {
      sum += row[k] * col[k];
    }
    temp.push(sum);
  }
  result.push(temp);
}

const ans = result.map((x) => x.join(" ")).join("\n");
console.log(ans);
```

## 풀이

1. a배열과 b배열 데이터 처리하기 -> shift() 메소드 사용.
2. b배열의 행과 열을 바꾸어주어서 행렬 곱을 처리하기 쉽도록 한 c배열을 만든다.
3. 마지막 3중 포문,, -> a배열에 행을 기준으로 c배열의 행(b배열의 열이므로 bM까지)을 가져와서 원소 하나씩 접근하여 2차원 배열을 만든다.
