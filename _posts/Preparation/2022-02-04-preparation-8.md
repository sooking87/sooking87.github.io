---
title: "[WEB] a 태그 밑줄 없애기 및 색상 변경"
excerpt: "[WEB] a 태그 밑줄 없애기 및 색상 변경"
categories: [Preparation]
tags: [Preparation, WEB, HTML/CSS/Javascript]
toc: true
toc_sticky: true
---

## 카테고리 밑줄 없애기 및 색상 변경

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="bGYeOeQ" data-user="sohnsookyoung" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/sohnsookyoung/pen/bGYeOeQ">
  project 3.2</a> by sohnsookyoung (<a href="https://codepen.io/sohnsookyoung">@sohnsookyoung</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

처음에는 span태그를 가지고 변경할려고 했는데 아마 제일 가까기 감싸진(?) 태그를 인식하는 것 같다. 그리고 a태그 색상 바꾸기를 검색해보니

- a:link {color:#} -> 아직 방문하지 않은 링크의 글자색 정의
- a:visited {color:#} -> 사용자가 방문한 적이 있는 링크의 글자색 정의
- a:hover {color:#} -> 마우스를 링크에 올려두었을 때, 글자색 정의
- a:active {color:#} -> 마우스로 링크를 클릭하고 뗄 때까지의 글자색 정의<br>

과 같은 css가 존재했다. 하지만 내가 하고 싶은 것은 현재 사용자가 들어가 있는 페이지만 색깔을 변경시키고 싶으니까 위 4가지 중 해당 사항은 없음.. 걍 기록차 적어놓는 것임! 또한 css내에 여러개를 적게 된다면 link -> visited -> hover -> active 순으로 작성해야 된다.

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="bGYeOeQ" data-user="sohnsookyoung" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/sohnsookyoung/pen/bGYeOeQ">
  project 3.2</a> by sohnsookyoung (<a href="https://codepen.io/sohnsookyoung">@sohnsookyoung</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>
<br>
뭐 안쓸줄 알았는데,,,ㅎ;;
