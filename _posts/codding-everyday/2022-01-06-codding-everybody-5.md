---
title: "[생활 코딩] 콘솔, 자료형, 변수와 대입 연산자, 제어할 태그 선택하기"
categories: ['생활 코딩']
tags: [생활 코딩, WEB]
toc: true
toc_sticky: true
---

## 콘솔
페이지에서 '검사'를 통해서 직접 열 수 있다. 콘솔창을 통해서 페이지 상의 워하는 값을 바로 출력할 수 있다. 생활 코딩에서는 페이스북 내에서 랜덤으로 4명 뽑기 등 실생활에서 필요한 바를 얻어내기 위한 코딩을 통해 배워보라고 하였다.<br>

## 자료형
자료형 중에서 숫자열과 문자열이 있다. 숫자열, 문자열 내가 알았던 바와 같다. 다만 C나 java와 달리 문자열인 경우 "로 시작하면 "로 묶어주고, '로 시작하면 '로 묶어 줘야 되지만 <strong>두개의 별 차이는 없다.</strong>
글자 수를 알아내기 위해서는 <strong>str.length</strong>를 사용하였다. 뿐만 아니라 <strong>str.toUpperCase, str.indexOf(찾을 문자 또는 문자열)</strong>을 통해서 문자열 중에서 원하는 값만을
출력할 수 있다. 
https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String
-> 자세한 내용은 이곳을 통해서 검색할 수 있다.<br>

## 변수와 대입연산자
이 역시 다른 언어와 비슷한 내용을 가지고 있다. 하지만 다른 점은 <strong>변수 앞에 var이라는 variable의 약자를 적어주어서 보다 정확한 변수임을 나타내줘야 된다는 것</strong>이다. 

## 제어할 테그 선택하기
이 장에서 앞에서 배운 바를 융합하여 하나의 간단한 코드를 배웠다. 
<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="zYELOjJ" data-user="sooking87" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/sooking87/pen/zYELOjJ">
  2022-01-07-codding-everbody</a> by sohnsookyoung (<a href="https://codepen.io/sooking87">@sooking87</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>
<strong>document.querySelector('class, id, html태그')</strong>을 사용하면 css의 태그들을 JavaScript를 통해서 사용할 수 있다. css에서 배경 색깔을 바꾸기 위해서는 background-color을 사용해주었지만 JavaScript에서는 <strong>.style.backgroundColor</strong>을 사용해주었다.
위 소스 코드에서는 body태그의 배경색(backgroundColor)와 글자색(color)을 바꿀 수 있는 button을 만들었다. 
