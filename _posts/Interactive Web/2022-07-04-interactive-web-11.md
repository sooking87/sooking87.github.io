---
title: "[Section 09] Transition/Animation 이벤트"
excerpt: "[Section 09] Transition/Animation 이벤트"
categories: [Interactive Web]
tags: [Interactive Web, WEB]
toc: true
toc_sticky: true
---

## 🔮 Transition 이벤트

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="yLKNPKM" data-user="sohnsookyoung" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/sohnsookyoung/pen/yLKNPKM">
  09-01</a> by sohnsookyoung (<a href="https://codepen.io/sohnsookyoung">@sohnsookyoung</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

### 📍 CSS

화면을 클릭했을 때, 원의 중심이 클릭된 부분으로 올 수 있게 하는 방법

```css
/* 포인터가 상단좌측에 오도록 */
position: absolute;
left: 0;
top: 0;
/* 포인터가 원의 중심에 오도록 */
margin: -15px 0 0 -15px;
```

### 📍 script

```js
const ballElem = document.querySelector(".ball");

window.addEventListener("click", function (e) {
  ballElem.style.transform =
    "translate(" + e.clientX + "px, " + e.clientY + "px)";
});

ballElem.addEventListener("transitionend", function (e) {
  console.log(e.elapsedTime); // 재생되는데 얼마나 걸리는지 나옴
  console.log(e.propertyName); // 속성 이름 알기.
  ballElem.classList.add("end");
});

// transitionstart
```

- 클릭 이벤트의 속성: clientX, clientY => 마우스가 찍힌 위치를 알 수 있다.
- transitionend 이벤트 : transition이 끝난 후 발생하는 이벤트
- transitionstart 이벤트 : transition이 시작할 때 발생하는 이벤트
  <br>

transitionXX 이벤트 속성 <br>

- e.elapsedTime : 재생되는데 얼마나 걸리는지 나옴
- e.propertyName : 속성 이름 알기

## 🔮 Animation 속성

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="abYOVRK" data-user="sohnsookyoung" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/sohnsookyoung/pen/abYOVRK">
  09-02_first</a> by sohnsookyoung (<a href="https://codepen.io/sohnsookyoung">@sohnsookyoung</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

### 📍 css

animation 속성 복습 <br>

- @keyframes ball-ani: 애니메이션을 작동했을 때 어느 부분에 어떤 css를 넣을 것인지 넣는다.
- alternate: (0, 0) -> (200, 200) -> (0, 0) 가 한 세트로 이동하는 것처럼 보인다.
- forwards: 종료시점에서 다시 to 부분으로 오는 것이 아니라 종료 시점에서 딱 종료되도록 한다.

### 📍 script

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="JjLdOea" data-user="sohnsookyoung" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/sohnsookyoung/pen/JjLdOea">
  09-02_second</a> by sohnsookyoung (<a href="https://codepen.io/sohnsookyoung">@sohnsookyoung</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

클릭을 했을 때, animation 이 작동하도록 한 코드. <br>

js 에서 style 속성을 조정해도 되고, css에서 클래스 하나를 만드어서 그 클래스를 추가하는 방식으로 이벤트를 처리해주어도 된다. 여튼 이 코드에서는 js에서 style을 통해서 animation 을 추가하였다.

- animationstart 이벤트
- animationend 이벤트
- animationiteration 이벤트: 반복이 될 때부터 작동되는 이벤트
