---
title: "[백준 9047번] 6147"
excerpt: "[백준 9047번] 6147"
categories: [Backjoon JavaScript]
tags: [Backjoon, JavaScript]
toc: true
toc_sticky: true
---

```javascript
let input = require("fs").readFileSync("example.txt").toString().split("\n");
let n = Number.parseInt(input[0]);

for (let i = 1; i <= n; i++) {
  let cnt = 0;
  let num = input[i];
  while (true) {
    if (Number.parseInt(num) === 6174) {
      console.log(cnt);
      break;
    }

    let splitArr = num.trim().split("").sort(); //String.trim() : 줄바꿈을 포함하여 문자열의 시작과 끝에서 공백을 제거합니다.
    let splitArr2 = splitArr;

    let min = Number.parseInt(splitArr2.join(""));
    let max = Number.parseInt(splitArr.reverse().join(""));
    num = (max - min).toString();

    if (num.length !== 4) {
      if (num.length === 3) {
        num = "0" + num;
      } else if (num.length === 2) {
        num = "00" + num;
      } else {
        num = "000" + num;
      }
    }
    cnt++;
  }
}
```

## 풀이 및 배운 점

1. String.trim() : 앞뒤 공백을 지워준다.
2. arr.reverse() / arr.join("")
3. Number.toString() : 숫자열을 문자열로 바꾸어 준다.

그리고 처음에 이 문제가 시간 초과가 나왔던 이유는 재배열해서 나올 수 있는 가장 큰 수에서 가장 작은 수를 뺐을 때, 그 수가 무조건 4자리 수는 아닐 수 있으므로 이를 조정해주어야 한다. 코드에서는 if - elseif - else문을 통해서 조정해주었다.
