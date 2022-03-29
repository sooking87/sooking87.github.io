---
title: "[백준 10809번] 알파벳 찾기"
excerpt: "[백준 10809번] 알파벳 찾기"
categories: [Backjoon JavaScript]
tags: [Backjoon, JavaScript]
toc: true
toc_sticky: true
---

```javascript
let input = require("fs").readFileSync("example.txt").toString();

//a = 97, z = 122

let ans = [];
for (let i = 97; i <= 122; i++) {
  ans.push(input.indexOf(String.fromCharCode(i)));
}
console.log(ans.join());
```

## 문제 풀이

js에서는 따로 데이터형이 없기 때문에 int n = 'a'처럼 자동으로 아스키 코드로 변환이 안된다. 따라서 String.fromCharCode를 통해서 아스키 코드를 알파벳을 만들어 준다.
indexOf는 배열, 문자열에서 값이 있다면 인덱스를 반환해주는 메소드이다.
