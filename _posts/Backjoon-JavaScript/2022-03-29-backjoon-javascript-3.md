---
title: "[백준 1546번] 평균"
excerpt: "[백준 1546번] 평균"
categories: [Backjoon JavaScript]
tags: [Backjoon, JavaScript]
toc: true
toc_sticky: true
---

```javascript
let input = require("fs").readFileSync("example.txt").toString().split("\n");

let n = parseInt(input[0]);
let scores = input[1].split(" ");
let newScore = 0;

scores.sort(function (a, b) {
  return a - b; //a가 크다면 양수, b가 크다면 음수
});

let max = scores[n - 1];
for (let i = 0; i < scores.length; i++) {
  newScore += parseInt(scores[i]);
}
newScore = ((newScore / max) * 100) / n;
console.log(newScore);
```

## 문제 풀이

점수를 뻥튀기 시키는 문제. 나 같은 경우는 sort를 통해서 최대값을 구했지만, 원래 있는 메소드인 Math.max를 사용해서 점수의 최댓값을 구해도 ㄱㅊ을 듯. 그리고 평균같은 경우는 늘어난 점수를 하나씩 계산해도 되지만, 공통 변수를 묶어서 계산하는 방법을 택했다.
