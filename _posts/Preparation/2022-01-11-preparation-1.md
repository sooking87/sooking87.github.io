---
title: "[WEB] table 태그"
excerpt: "[WEB] table 태그"
categories: [Preparation]
tags: [Preparation, WEB, HTML/CSS/Javascript]
toc: true
toc_sticky: true
---

## 계산기 만들기

계산기 틀을 만들기 위해서는 먼저 숫자들을 4행 3열로 배치를 시켜야된다. 이를 위해서 display: grid;를 사용하려고 했지만 구글링을 해보니 **table** 이라는 태그를 발견했다. 표를 만드는 태그를 통해서 계산기를 만들어볼 수 있을 것 같았다.<br>

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="Exwdeyq" data-user="sooking87" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/sooking87/pen/Exwdeyq">
  table tags</a> by sohnsookyoung (<a href="https://codepen.io/sooking87">@sooking87</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>
### table 태그
1. table: 테이블 태그 시작할 때 사용, border=1을 해야 테이블에 선이 그어진다.
2. th: table head의 약자로 표 제목에 사용
3. td: table data의 약자로 표 안의 내용을 입력할 때 사용
4. tr: table row로 tr태그 안에 있는 th/td태그들을 가로로, tr태그들은 세로로 배열된다.
5. colspan, rowspan: 엑셀의 병합과 같은 역할

### Java Script

1. document.ElementById('id').value
   자바 스크립트가 어려웠다. 숫자를 눌렀을 때, 누른 숫자가 입력이 되야됬다. 창에서 입력된 값을 js로 불러오기 위해서는 **document.getElementById('id')** 를 사용했다. 하지만 **document.getElementById('id')** 는 해당 id의 html만 불러오는 듯 했다. 그래서 그 '값'을 가져오기 위해서는 **.value** 까지 붙혀줘야 한다. 코드 진행 과정은 **onclick(숫자 클릭) -> onclick="!이 부분이 실행!" -> 코드 상에는 함수가 있으므로 해당 함수로 이동 -> (계산 후 출력하기 위해서는)계산한 값을 출력될 창의 id를 통해서 값 전달 -> 출력** **document.querySelector()** 와 비슷하지만 querySelector같은 경우는 괄호 안에 id, class다 올 수 있지만 getElementById는 괄호 안에 id밖에 오지 않는다. 클래스를 넣을 수 있는 getElementByClass도 있다.

### 코드 수정하고 싶은 부분

1. 표 작성시 반복이 너무 많아서 js를 통해서 함수를 만들어 줄여보고 싶다.
2. 테이블에 색감을 넣고 싶다.
3. AC, 0부분의 버튼의 크기 역시 딱 맞추고 싶다.
4. 함수들을 클래스에 넣어서 정리해 보자.
