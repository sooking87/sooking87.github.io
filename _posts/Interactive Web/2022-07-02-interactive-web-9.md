---
title: "[Section 07] 객체"
excerpt: "[Section 07] 객체"
categories: [Interactive Web]
tags: [Interactive Web, WEB]
toc: true
toc_sticky: true
---

## 🔮 객체 1

```js
const person = {};
// 속성, property :
person.name = "일분이";
person.age = 10;
person.introduce = function () {
  console.log("안녕하세요. 저는 일분이 이고 나이는 10살이에요.");
};
person.introduce();

const person2 = {
  name: "일분이",
  age: 10,
  introduceMySelf: function () {
    console.log("안녕?");
  },
};
person2.introduceMySelf();
```
