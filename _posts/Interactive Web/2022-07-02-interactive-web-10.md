---
title: "[Section 08] 스크롤 이벤트"
excerpt: "[Section 08] 스크롤 이벤트"
categories: [Interactive Web]
tags: [Interactive Web, WEB]
toc: true
toc_sticky: true
---

## 🔮 스크롤 이벤트 다루기

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="WNzvOOQ" data-user="sohnsookyoung" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/sohnsookyoung/pen/WNzvOOQ">
  08_02</a> by sohnsookyoung (<a href="https://codepen.io/sohnsookyoung">@sohnsookyoung</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

window객체의 **_pageYOffset_** 속성을 사용하여서 현재 스크롤을 얼마나 했는지 픽셀로 나타내준다.

## 🔮 스크롤 위치에 따라 오브젝트 조작하기

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="gOepGNQ" data-user="sohnsookyoung" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/sohnsookyoung/pen/gOepGNQ">
  08_03</a> by sohnsookyoung (<a href="https://codepen.io/sohnsookyoung">@sohnsookyoung</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

- ilbuniElem.offsetTop : ilbuniElem 의 위치가 위에서부터 얼마나 떨어져 있는지 알 수 있다.
- ilbuniElem.getBoundingClientRect() : ilbuni가 있는 위치를 가지고 있는 객체로, 스크롤을 내릴 때 어떤 동작을 하도록 하고 싶은 것이므로 위 코드에서는 top 속성을 사용하였다.
- window.innerHeight : 윈도우 화면의 높이를 구할 수 있다.
