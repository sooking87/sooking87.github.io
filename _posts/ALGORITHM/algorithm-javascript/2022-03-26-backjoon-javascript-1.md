---
title: "[백준 2480번] 주사위 세개"
excerpt: "[백준 2480번] 주사위 세개"
categories: [Algorithm JavaScript]
tags: [Algorithm Study, JavaScript, Algorithm, Backjoon]
toc: true
toc_sticky: true
---

```javascript
let input = require("fs").readFileSync("example.txt").toString().split(" ");
let nums = [];
let money = 0;
for (let i = 0; i < input.length; i++) {
  nums[i] = parseInt(input[i]);
}

nums.sort(function (a, b) {
  return a - b; //a가 크다면 양수, b가 크다면 음수
});

if (nums[0] === nums[1]) {
  if (nums[1] === nums[2]) {
    money = 10000 + nums[0] * 1000;
  } else {
    money = 1000 + nums[0] * 100;
  }
} else if (nums[1] === nums[2]) {
  money = 1000 + nums[1] * 100;
} else {
  money = nums[2] * 100;
}

console.log(money);
//'/dev/stdin'
```

## 문제 풀이

자바 스크립트는 주로 웹을 만들 때 사용하기 때문에 알고리즘 문제를 푸는데 특화되어 있지는 않다. 하지만 자바 스크립트의 기본 문법을 익히기 위해서 백준 문제풀이를 진행했다. 이 문제는 같은지 다른지를 비교하기 전에 세 주사위가 모두 다르다면 제일 큰 숫자를 결국 찾아야 되기 때문에 정렬 후, 비교를 시작했다.
