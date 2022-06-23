---
title: "[Section 02] CSS 3D #2"
excerpt: "[Section 02] CSS 3D #2"
categories: [Interactive Web]
tags: [Interactive Web, WEB]
toc: true
toc_sticky: true
---

# CSS 3D

## 🔮 CSS 3D #2

마우스를 위에 올리면 카드가 돌아가는 것 처럼 보이게 하기

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="jOZgOPz" data-user="sohnsookyoung" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/sohnsookyoung/pen/jOZgOPz">
  Untitled</a> by sohnsookyoung (<a href="https://codepen.io/sohnsookyoung">@sohnsookyoung</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>
<br>

여기서 처음 .card의 transform을 0도로 굳이 안해놓아도 되지만 해놓는 것이 좋다고 한다. 움직일 준비를 시킨다. => 성능에 도움을 준다.

## 🔮 앞 뒤 다른 카드 만들기

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="jOZgOPz" data-user="sohnsookyoung" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/sohnsookyoung/pen/jOZgOPz">
  Untitled</a> by sohnsookyoung (<a href="https://codepen.io/sohnsookyoung">@sohnsookyoung</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

### 📍 설명

- html
  기존에는 카드 클래스를 3개를 만들었다면 해당 카드 클래스 안에 앞과 뒤에 해당하는 카드를 만들어준다. .card-side를 통해서 공통 스타일을 적용시키고 앞과 뒤에 각각 해당하는 스타일은 .card-side-front, .card-side-back을 통해서 적용시킬 수 있다.
- css

  - 카드를 겹치는 방법 <br>
    카드 컨테이너 클래스인 .card에서는 **_position: relative;_** 를 통해서 .card를 기준으로 배치가 되도록 하고, .card-side에서 부모 요소를 기준으로 배치시키기 위해서 **_position: absolute;_** 를 사용한다. 그렇게 된다면 앞장과 뒷장 모두 left: 0, top: 0에 위치하므로 카드가 겹치게 된다.
    <p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="jOZgOPz" data-user="sohnsookyoung" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
    <span>See the Pen <a href="https://codepen.io/sohnsookyoung/pen/jOZgOPz">
    Untitled</a> by sohnsookyoung (<a href="https://codepen.io/sohnsookyoung">@sohnsookyoung</a>)
    on <a href="https://codepen.io">CodePen</a>.</span>
    </p>
    <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

  - 마우스를 올리면 카드 뒷장이 보이게 하기 <br>

    1. 지금 .world의 자식 요소에만 3d가 적용되고 있는 상태이므로 card-side-front, card-side-back 모두 3d가 유지되도록 하기 위해서 .card-side에도 마찬가디로 .world의 3d가 유지되도록 **_transform-style: preserve-3d;_** 을 사용한다.
    2. 마우스를 위로 올렸을 때, 뒷 장이 보이도록 하기 위해서 **_backface-visibility: hidden;_** 을 사용한다.

    <p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="jOZgOPz" data-user="sohnsookyoung" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
    <span>See the Pen <a href="https://codepen.io/sohnsookyoung/pen/jOZgOPz">
    Untitled</a> by sohnsookyoung (<a href="https://codepen.io/sohnsookyoung">@sohnsookyoung</a>)
    on <a href="https://codepen.io">CodePen</a>.</span>
    </p>
    <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

  - 문처럼 열리고 닫히는 것 처럼 만들기
    **_transform-origin: left;_** 을 사용해서 회전 중심이 왼쪽이 되도록 하고, 앞쪽으로 열리는 것 처럼 하기 위해서 마우스를 올렸을 때 돌아가는 각도를 **_-180deg_** 로 한다.

    <p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="jOZgOPz" data-user="sohnsookyoung" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
    <span>See the Pen <a href="https://codepen.io/sohnsookyoung/pen/jOZgOPz">
    Untitled</a> by sohnsookyoung (<a href="https://codepen.io/sohnsookyoung">@sohnsookyoung</a>)
    on <a href="https://codepen.io">CodePen</a>.</span>
    </p>
    <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>
