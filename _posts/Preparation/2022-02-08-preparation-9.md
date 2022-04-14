---
title: "[WEB] flex 속성"
excerpt: "[WEB] flex 속성"
categories: [Preparation]
tags: [Preparation, WEB, HTML/CSS/Javascript]
toc: true
toc_sticky: true
---

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="KKyaary" data-user="sohnsookyoung" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/sohnsookyoung/pen/KKyaary">
  Untitled</a> by sohnsookyoung (<a href="https://codepen.io/sohnsookyoung">@sohnsookyoung</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

다음과 같은 html에 flex 속성을 적용시켜보자
<br>

부모 요소인 div.container를 플렉스 컨테이너라고 부르고, 자식 요소인 div.item을 플렉스 아이템이라고 부른다. 컨테이너가 Flex의 영향을 받는 전체 공간이고, 설정된 속성에 따라 각 아이템들이 배치가 된다.

# 컨테이너에 적용하는 속성

#### display: flex;

딱 내용물 만큼의 너비만큼씩 공간이 배치된다.

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="abVppxX" data-user="sohnsookyoung" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/sohnsookyoung/pen/abVppxX">
  Untitled</a> by sohnsookyoung (<a href="https://codepen.io/sohnsookyoung">@sohnsookyoung</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script><br>

inline-flex 같은 경우는 컨테이너가 아이템들의 크기에 맞춰 바뀐다. 그냥 flex인 경우에는 컨테이너 크기는 고정, 안에 아이템들의 크기만 글씨 크기만큼의 너비를 가지는 반면, inline-flex같은 경우는 안에 아이템들의 크기만큼에 너비에 따라서 컨테이너의 크기도 바뀐다.

#### flex-direction

- flex-direction: row; -> 아이템들이 가로 방향으로 배치
- flex-direction: row-reverse -> 아이템들이 역순으로 가로 배치
- flex-direction: column -> 아이템들이 세로 방향으로 배치
- flex-directionL: column-reverse -> 아이템들이 역순으로 세로 배치

#### flex-wrap

컨테이너가 더 이상 아이템들을 한 줄에 담을 여유 공간이 없을 때 아이템 줄바꿈을 어떻게 할지 결정하는 속성<br>

- flex-wrap: nowrap; -> 아이템이 삐져나감
- flex-wrap: wrap; -> 아이템이 삐져나갈 경우, 줄바꿈을 함
- flex-wrap: wrap-reverse; -> 줄바꿈을 하는데 reverse함,,,ㅎ

#### flex-flow

flex-direction과 flex-wrap을 한꺼번에 지정할 수 있는 단축 속성<br>

- flex-flow: row wrap; 와 같이 사용
  <br>

### 메인축을 정렬하는 속성

#### justify-content

- justify-content: flex-start; -> 앞에서부터 아이템들 시작
- justify-content: flex-end;
- justify-content: center;
- justify-content: space-between; -> 아이템들의 사이에 균일한 간격을 만들어 준다.
- justify-content: space-around; -> 아이템들의 둘레에 군일한 간격을 만들어 준다.
- justify-content: space-evenly; -> 아이템들의 사이와 양끝에 균일한 간격을 만들어 준다. **이거 사용할 듯!**

### 수직축을 정렬하는 속성

#### align-items

- align-items: stretch; -> 아이템들이 수직축 방향으로 끝까지 늘어남
- align-items: flex-start; -> 아이템들을 시작점으로 정렬 이때, 높이는 글씨 크기만큼!
- align-items: flex-end;
- align-items: center;
- align-items: baseline; -> 글씨가 가장 큰 높이를 기준으로 밑부분을 맞춤

#### align-content

**flex-wrap: wrap;인 상태에서 적용 가능**

- align-content: strech;
- align-content: flex-start;
- align-content: flex-end;
- align-content: center;
- align-content: space-between;
- align-content: space-around;
- align-content: space-evenly;
  <br>

아까 컨테이너 안에 있는 아이템들간의 공간을 설정할 때 쓰였던 space-between, around, evenly지만 위의 속성같은 경우는 아이템을 정렬하는 속성이므로 아이템과 아이템 간의 위아래 간격을 결정 _아까 컨테이너의 속성인 경우는 아이템과 아이템 간의 양옆 간격을 결정_

# 아이템에 적용하는 속성들

#### flex-basis

Flex 아이템의 기본 크기를 설정. flex-direction이 row일 때는 너비, coulumn일 때는 높이를 설정

#### flex-grow

유연하게 늘리기.

#### flex-shrink

유연하게 줄이기

**grow, shrink속성은 많이 사용할 듯!**
<br>

### 수직축으로 아이템 정렬

#### align-self

- align-self: auto;
- align-self: stretch;
- align-self: flex-start;
- align-self: flex-end;
- align-self: center;
- align-self: baseline;
  적용 부분은 컨테이너 적용 속성 중 align-items와 똑같.<br>

위 내용은 `https://studiomeal.com/archives/197`에서 참고하였음을 밝힙니다.
