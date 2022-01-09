---
title: "[생활 코딩] 객체 예고 ~ 라이브러리와 프레임워크"
categories: [생활 코딩]
tags: [생활 코딩, WEB]
toc: true
toc_sticky: true
---
## 객체
앞에서 함수에 대해서 배웠다. 함수를 사용함으로써 반복을 줄이고 유지, 보수를 쉽게 할 수 있다. 하지만 이런 함수들을 모아서 더욱 가독성을 높이는 것이 객체이다. 요즘 자바를 공부하면서 객체에 대해서 배우고 있다. 객체를 효율적으로 사용한다면 활용도 높고, 가독성 높은 코드를 구현할 수 있다.
<div class="colorscripter-code" style="color:#f0f0f0;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px;border-right:2px solid #4f4f4f"><div style="margin:0;padding:0;word-break:normal;text-align:right;color:#aaa;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="line-height:130%">1</div><div style="line-height:130%">2</div><div style="line-height:130%">3</div><div style="line-height:130%">4</div><div style="line-height:130%">5</div></div></td><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#f0f0f0;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#ff3399">var</span>&nbsp;객체변수&nbsp;이름&nbsp;<span style="color:#aaffaa"></span><span style="color:#ff3399">=</span>&nbsp;{</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#ffd500">"key"</span>:<span style="color:#ffd500">"value"</span>&nbsp;,</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#ffd500">"key2"</span>:<span style="color:#ffd500">"value2"</span>,</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;...</div><div style="padding:0 6px; white-space:pre; line-height:130%">};</div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#4f4f4f;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div><br>
위의 코드는 객체 변수를 위한 기본 문법이다. 객체에 다른 원소를 추가하고 싶다면 **객체변수 이름.key = "value";** 이렇게 대입해주면 된다. 또한 key값에 띄어쓰기가 있다면 **객체변수 이름["key"] = "value";** 이렇게 배열 형태로 key값을 설정해주면 된다.
<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="vYezdNz" data-user="sooking87" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/sooking87/pen/vYezdNz">
  js5</a> by sohnsookyoung (<a href="https://codepen.io/sooking87">@sooking87</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script><br>
화면창에 출력하기 위해서는 **document.write();** 를 쓰면되고, 객체의 값을 출력하기 위해서는 **coworkers.programmer** 을 사용해주면 된다. 하지만 지금은 객체 내의 값이 별로 없기 때문에 직접 하나하나 다 출력할 수 있지만, 그 수가 많아지게 된다면 직접 출력하는데는 무리가 생긴다. 이때, 반복문을 사용해서 출력해줄 수 있다.
<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="eYGLyqz" data-user="sooking87" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/sooking87/pen/eYGLyqz">
  js4</a> by sohnsookyoung (<a href="https://codepen.io/sooking87">@sooking87</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script><br>
위의 Iterate해더 아래는 결국 같은 결과를 출력하고 있지만 반복문을 통해서 훨씬 더 효율적인 코드를 만들었다. 반복문 내의 조건은 coworkers 객체 안에 있는 key값이 변수가 된다. 따라서 값(value)를 출력하고 싶다면 **객체변수[key]** 를 사용해서 출력해줄 수 있다. 배열에서 인덱스를 통해서 배열의 원소를 하나씩 출력하는 형식과 비슷하다. 하지만 인덱스와 다른 점은 **key값은 항상 정수형이 아니라는 것이다.** 이런 객체에는 값뿐만 아니라 함수도 들어갈 수 있다. 비슷한 역할을 하는 함수들끼리 묶어서 객체로 정리할 수 있다는 것이다. 함수를 객체에 대입하는 과정은 다음과 같다.
<div class="colorscripter-code" style="color:#f0f0f0;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px;border-right:2px solid #4f4f4f"><div style="margin:0;padding:0;word-break:normal;text-align:right;color:#aaa;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="line-height:130%">1</div><div style="line-height:130%">2</div><div style="line-height:130%">3</div></div></td><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#f0f0f0;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%">객체변수&nbsp;이름.함수이름&nbsp;<span style="color:#aaffaa"></span><span style="color:#ff3399">=</span>&nbsp;<span style="color:#ff3399">function</span>(매개변수)&nbsp;{</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;함수&nbsp;기능&nbsp;코드;</div><div style="padding:0 6px; white-space:pre; line-height:130%">}</div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#4f4f4f;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div><br>
이를 이용해서 객체들의 값을 출력해주는 함수를 객체에 추가해보았다.
<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="XWePZKR" data-user="sooking87" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/sooking87/pen/XWePZKR">
  Untitled</a> by sohnsookyoung (<a href="https://codepen.io/sooking87">@sooking87</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script><br>

## 파일로 쪼개서 정리 정돈
**소스코드 > 함수 > 객체 > 파일** 순으로 코드를 정리할 수 있다. 파일로 정리하는 방법은 자바 스크립트에 대한 내용만 빼서 따러 .js파일을 만들어 준다. 그 후 **src = 파일명.js** 를 추가해주면 된다.
<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="dyVqdOK" data-user="sooking87" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/sooking87/pen/dyVqdOK">
  js_final</a> by sohnsookyoung (<a href="https://codepen.io/sooking87">@sooking87</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script><br>

## 의문점
1. 함수에서 사용되는 this와 self는 무엇일까?
2. css파일도 따로 빼서 파일로 정리할 수 있을까? -> 저번에 coffee story 만들어볼 때, 꼭 필요함을 느낌,,,
