---
title: "[백준 1427번] 소트인사이드"
excerpt: "[백준 1427번] 소트인사이드"
categories: [Backjoon JavaScript]
tags: [Backjoon, JavaScript]
toc: true
toc_sticky: true
---

```js
let input = require("fs").readFileSync("example.txt").toString().split("");

// 문자열 정렬 -> 각 자리수는 0~9까지 가능하므로 문자열로 정렬해도 원하는 대로 나옴
input.sort(); // 오름차순
var answer = "";

// 오름차순 정렬이 된 input을 인덱스를 거꾸로 하여 내림차순 문자열로 만든다.
for (var i = input.length - 1; i >= 0; i--) {
  answer += input[i];
}

console.log(answer);
//3 10 -> 10 3
```

## 풀이

js의 경우는 sort 메소드가 문자열 기준으로 정렬을 정의하고 있기 때문에 이를 이용하여 굳이 숫자형으로 안바꿔도 정렬이 가능하다. 사실 js는 데이터형 상관 없긴 하지만,,,그리고 문자끼리 붙혀주는 것 역시 += 연산자를 사용하여 진행.
