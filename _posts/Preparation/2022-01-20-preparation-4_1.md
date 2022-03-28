---
title: "[WEB] 미디어 쿼리 적용"
excerpt: "[WEB] 미디어 쿼리 적용"
categories: [Preparation]
tags: [Preparation, WEB, HTML/CSS/Javascript]
toc: true
toc_sticky: true
---

## 수정 사항 1. 미디어 쿼리 성공

처음에는 span, table, textarea, span 이렇게만 두고 열은 1fr 5fr 1fr이렇게 두었기 때문에 textarea가 옆으로 딸려 올라왔던 것이다. 따라서 table 태그를 span으로 감쌌고, textarea를 span으로 감쌌다. 그럼에도 원하는 대로 나오지 않았던 이유는 계산기와 출력기의 시작, 끝 그리드 값을 입력하지 않아서 그랬다. <br>
이렇게 문제를 해결했다고 생각했는데 계산기와 출력기가 위아래로 동시에 배치되지 않는 문제가 생겼다. css는 위에서부터 순차적으로 웹에 적용이 되기 때문에 미디어쿼리를 이용하더라도 변경되는 값들이 있는 태그들보다 아래에 위치시켜야 된다.

## 수정 사항 2. .js파일 따로 정리

이 부분은 깃허브 Calculator 레퍼토리에 저장해 놓았다.

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="poWmQXX" data-user="sooking87" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/sooking87/pen/poWmQXX">
  cal2</a> by sohnsookyoung (<a href="https://codepen.io/sooking87">@sooking87</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>
끝~~~!
