---
title: "[WEB] textarea 출력 방식"
excerpt: "[WEB] textarea 출력 방식"
categories: [Preparation]
tags: [Preparation, WEB, HTML/CSS/Javascript]
toc: true
toc_sticky: true
---

## 수정 사항 1. 함수들을 리스트로 정리

## 수정 사항 2. textarea에는 "="을 눌러고 출력값은 그대로 유지시키기

이거 수정하는데 꽤 오래 걸렸다. 처음에는 리스트에 계산식을 다 넣고, 반복문을 통해서 하나씩 **document.getElementById('output') = operations[i]** 를 통해서 textarea에 출력해주면 될 줄 알았다. 하지만 textarea에는 하나의 문자열만을 출력할 수 있는 것 같았다. 결국 리스트를 이용하였다면 계속 마지막의 계산식만을 출력해주는 것이었다. 따라서 _operationsString_ 이라는 변수를 사용하여서 이 변수에 리스트에 있는 값들을 다 더해(?) 주었다. 그랬더니 수정하고 싶은 사항 해결!했다. <br>

## 수정 사항 3. 계산기 "옆에" textarea띄우기

이거는 계산기와 textarea를 하나의 div 태그로 묶은 후, style 태그 안에 **display: grid** 를 통해서 병렬로 화면을 띄울 수 있었다. <br>
<br>

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="LYzoPoV" data-user="sooking87" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/sooking87/pen/LYzoPoV">
  operations</a> by sohnsookyoung (<a href="https://codepen.io/sooking87">@sooking87</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>
### 코드 수정하고 싶은 부분
1. 표 작성시 반복이 너무 많아서 js를 통해서 함수를 만들어 줄여보고 싶다. -> 굳이 필요할까라는 생각이 든다. 계산기의 숫자는 고정되어있기 때문이다.
2. 테이블에 색감을 넣고 싶다. -> 2022.01.15 수정 완료👌
3. AC, 0부분의 버튼의 크기 역시 딱 맞추고 싶다. -> 2022.01.15 수정 완료👌
4. 함수들을 클래스에 넣어서 정리해 보자. -> 2022.01.19 수정 완료👌
5. 계산기 옆에 계산한 사항들을 적고싶다. '='을 누르면 창 제일 위부터 출력됨 -> AC를 눌러도 이 부분은 계속 남아있으면서 동시에 "<reset>"표시가 뜨도록 만들고 싶다. -> 2022.01.19 수정 완료👌
6. 계산기 "옆에" 출력창을 두고 싶다. -> 2022.01.19 수정 완료👌
7. 화면의 크기에 따라 계산기와 textarea위치 변경(미디어 쿼리 이용)
8. .js파일 형태로 따로 빼서 만들기
9. AC가 눌러지기 전까지 "="가 눌러지면 계산값은 다시 위쪽의 input 태그로 넘어가기 -> 가능할지는 모르겠다...빨리 p5.js써서 게임 만들기를 해보고 싶기 때문,,그래도 안하면 찜찜할 것 같아서 하긴 할 듯,,<br>
### 목표
1월 가기 전까지 개인 프로젝트(?) 2개는 해보기!
