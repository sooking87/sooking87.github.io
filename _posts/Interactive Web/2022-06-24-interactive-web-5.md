---
title: "[Section 03] CSS Flex"
excerpt: "[Section 03] CSS Flex"
categories: [Interactive Web]
tags: [Interactive Web, WEB]
toc: true
toc_sticky: true
---

## 🔮 Flex Box

### 📍 기본 flex 속성

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="PoQMbrG" data-user="sohnsookyoung" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/sohnsookyoung/pen/PoQMbrG">
  03_01_first</a> by sohnsookyoung (<a href="https://codepen.io/sohnsookyoung">@sohnsookyoung</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>
<br>

flex의 기본 모양은 지정해놓은 컨테이너에 맞게 높이가 지정이 되며 가로로 배치가 된다.

### 📍 flex-direction

```css
.container {
  display: flex;
  flex-direction: row;
  height: 80vh;
  background: gray;
}
.item {
  padding: 2em;
  border: 3px solid black;
  background: white;
}
```

row가 디폴트, 꼬치를 행 방향으로 꽂으면 아이템이 꽂힌 방향대로 나온다.
<br>

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="WNMVoqE" data-user="sohnsookyoung" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/sohnsookyoung/pen/WNMVoqE">
  03_01_second</a> by sohnsookyoung (<a href="https://codepen.io/sohnsookyoung">@sohnsookyoung</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>
<br>

반대로 **_flex-direction: column_** 인 경우 꼬치가 열 형태로 꽂히면 아이템이 다음과 같이 정렬됨을 알 수 있다.

### 📍 justify-content

어묵을 꼬치 위에서 정렬하는 방법 ㅋㅋ

- flex-start: default
- flex-end
- center
- space-between: **맨 앞 아이템과 맨 뒤 아이템은 컨테이너 양 끝에 붙고** , 그 외의 아이템 사이에 균일한 여백을 준다.
- space-evenly: **맨 앞 아이템과 맨 뒤 아이템 포함** 컨테이너의 공간에 균일하게 여백을 준다.
- space-around: 각 아이템 주변에 특정 여백이 주어진다.

### 📍 align-items

기본 축 기준으로 수직 방향으로 아이템들을 정렬하는 방법

- stretch: default
- flex-start
- flex-end
- center

### 📍 flex-grow

컨테이너의 크기에 맞게 꽉 차도록 만들어주는 속성. 속성값으로는 그냥 숫자만 있으면 된다. <br>

각각의 아이템 별로 다른 비율을 주고 싶다면 다음과 같이 하면 된다.

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="abqepOx" data-user="sohnsookyoung" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/sohnsookyoung/pen/abqepOx">
  Untitled</a> by sohnsookyoung (<a href="https://codepen.io/sohnsookyoung">@sohnsookyoung</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>
<br>

**_nth-child(N)_** 이라는 것은 부모 속성에 몇 번째 요소인지를 나타낸다.
<br>

이 속성의 경우는 컨테이너를 꽉 차게 해주는데, 자신의 content를 제외한 나머지 공백을 동일한 비율 또는 특정 비율로 나누어 갖는 것을 말한다.

### 📍 flex-basis

여기서 의도한 대로 정확히 아이템들을 동일한 칸을 차지하도록 하기위해서는 **_flex-basis:0_** 을 이용해 준다.

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="LYQwxNY" data-user="sohnsookyoung" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/sohnsookyoung/pen/LYQwxNY">
  Untitled</a> by sohnsookyoung (<a href="https://codepen.io/sohnsookyoung">@sohnsookyoung</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>
