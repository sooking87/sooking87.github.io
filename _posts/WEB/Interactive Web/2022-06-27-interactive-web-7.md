---
title: "[Section 05] 자바스크립트 이벤트 다루기"
excerpt: "[Section 05] 자바스크립트 이벤트 다루기"
categories: [Interactive Web]
tags: [Interactive Web, WEB]
toc: true
toc_sticky: true
---

## 🔮 이벤트 기본 조작

```js
const ilbuni = document.querySelector(".ilbuni.c");
ilbuni.addEventListener("click", function () {
  ilbuni.classList.toggle("special");
});
```

조작하고자 하는 DOM을 가져와서 **_addEventListener(type, function, options)_** 를 해준다.

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="BarBqKe" data-user="sohnsookyoung" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/sohnsookyoung/pen/BarBqKe">
  05_01</a> by sohnsookyoung (<a href="https://codepen.io/sohnsookyoung">@sohnsookyoung</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>
 
 <br>

근데 여기서 script 태그를 head 태그 안에 넣어주기 위해서는 페이지 로드가 끝나고 script 태그가 로드되어야 하므로 load 클래스를 사용한다. <br>

```js
window.addEventListener("load", function () {
  const ilbuni = document.querySelector(".ilbuni.c");
  ilbuni.addEventListener("click", function () {
    ilbuni.classList.toggle("special");
  });
});
```

근데 이렇게 하면 모든 페이지가 로드된 이후에 작동이 되므로 비효율적이다.

### 📍 효율적으로 head 태그 안에 script 태그 넣기

```js
window.addEventListener("DOMContentLoaded", function () {
  const ilbuni = document.querySelector(".ilbuni.c");
  ilbuni.addEventListener("click", function () {
    ilbuni.classList.toggle("special");
  });
});
```

**_DOMContentLoaded_** 를 사용해준다. DOMContentLoaded를 사용해주면 돔이 로드가 된다면 바로 이벤트 리스너를 사용할 수 있도록 해준다.

### 📍 RULE 1. body 태그에 script 태그 넣어주기

요즘은 이 방법을 더 많이 쓴다고 한다.

### 📍 RULE 2. 전역 변수를 최소화 하자

그래서 전역 변수를 최소화하기 위해서 작성해두었던 코드를 다시 함수로 감싸서 지역 변수로 만들어 준다. 이때 함수 이름이 붙으면 다시 그 함수는 전역 변수가 되므로 이름이 없는 함수를 만들어 준다.

```js
(function () {
  const ilbuni = document.querySelector(".ilbuni.c");
  const clickInbuniHandler = () => {
    ilbuni.classList.toggle("special");
  };
  ilbuni.addEventListener("click", clickInbuniHandler);
})();
```

## 🔮 this와 이벤트 객체

```js
(function () {
  const characters = document.querySelector(".characters");
  function clickHandler(e) {
    console.log(e.currentTarget);
    console.log(e.target);
  }
  characters.addEventListener("click", clickHandler);
})();
```

이벤트에 추가된 메소드의 경우 자동으로 e라는 매개변수가 추가된다.
<br>

- e.currentTarget: this와 e.currentTarget은 이벤트가 등록되어있는 객체를 가리킨다.
- e.target: e.target의 경우는 내가 클릭한 객체가 무엇인지를 알 수 있다.

## 🔮 움직이는 캐릭터 예제로 클릭 이벤트 익혀보기

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="xxWKQEM" data-user="sohnsookyoung" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/sohnsookyoung/pen/xxWKQEM">
  05_03</a> by sohnsookyoung (<a href="https://codepen.io/sohnsookyoung">@sohnsookyoung</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

## 🔮 이벤트 위임

### 📍 반복문을 통해서 이벤트 리스너를 등록한 것은 비효율이다.

💡 sol: 부모 DOM에 이벤트 리스너를 등록하고 e.target을 사용해서 자식 노드에 이벤트를 적용시킨다.
<br>

❗ 문제점: 자식 노드 외의 다른 stage 공간이 클릭이 된다면 에러가 뜬다.
<br>

💡 sol: 조건문을 통해서 예외처리를 해준다. => **_classList.contains('클래스이름')_**
<br>

최종.js

```js
(function () {
  const stage = document.querySelector(".stage");
  function clickHandler(e) {
    if (e.target.classList.contains("ilbuni")) {
      stage.removeChild(e.target);
    }
  }
  stage.addEventListener("click", clickHandler);
})();
```

### 📍 이벤트 위임 받은 객체 안에 또 객체가 있는 경우

- pointer-events: none;: 클릭 이벤트를 받지 않는다. => 간단한 구조에서는 상관 없지만 하위에 있는 요소에 대한 다른 클릭 이벤트가 필요하다면 아래와 같은 클릭 이벤트 메소드를 작성해줄 수 있다.
- ```js
  function clickBtnHandler(e) {
    let elem = e.target;
    while (!elem.classList.contains("menu-btn")) {
      elem = elem.parentNode;
      if (elem.nodeName === "BODY") {
        elem = null;
        return;
      }
    }
  }
  ```
