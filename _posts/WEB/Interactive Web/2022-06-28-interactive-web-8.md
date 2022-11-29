---
title: "[Section 06] 예제) 3개의 문"
excerpt: "[Section 06] 예제) 3개의 문"
categories: [Interactive Web]
tags: [Interactive Web, WEB]
toc: true
toc_sticky: true
---

## 1️⃣ 레이아웃 잡기

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="PoRomMo" data-user="sohnsookyoung" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/sohnsookyoung/pen/PoRomMo">
  06_01</a> by sohnsookyoung (<a href="https://codepen.io/sohnsookyoung">@sohnsookyoung</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

1. .stage 배경색 채우기
2. outline 속성을 통해서 문의 위치를 display: flex로 정렬시키기
3. 검정 배경 위에
4. 이미지 위에
5. 문 넣기

## 2️⃣ transition, transform 속성 사용하기(html, CSS까지만 사용)

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="MWVWobO" data-user="sohnsookyoung" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/sohnsookyoung/pen/MWVWobO">
  06_02</a> by sohnsookyoung (<a href="https://codepen.io/sohnsookyoung">@sohnsookyoung</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

1. 원래 이미지들이 문 오른쪽에 있다가 나타나야되므로 -> .ilbuni 에 `transform: translate3d(100%, 0, 0);` 을 넣어서 이미지 크기만큼 한 칸씩 오른쪽으로 밀리도록 한다. 그리고 오른쪽으로 가 있으면 안보여야 되므로 `overflow: hidden;` 을 사용해준다.
2. 원래는 클릭하면 문이 열리는 것이지만 일단 테스트해보기 위해서 마우스를 문 위에 올렸을 때를 기준으로 만들어 본다.
   1. .door에 마우스를 올리면 .door-body가 -110deg 만큼 움직인다. 문이 열리는 것 처럼 보이기 위해서 차원을 넣어준다. 여기서 .door을 감싸고 있는 .stage 에 차원을 넣어준다면 열렸을 때 다 같은 모양으로 열리는 것이 아니므로 **열리는 객체에** 차원을 넣어준다.
   2. 문이 열리면 스폰지밥을 보여주기 위해서 transform을 다시 원래대로 돌려놓고 `transition: 0.5s 0.3s;` 을 이용하여 문이 열리고 0.3s 후에 0.5s 만큼 동작하도록 한다.

## 3️⃣ 클릭했을 때 문 열리게 하기

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="eYMYRyK" data-user="sohnsookyoung" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/sohnsookyoung/pen/eYMYRyK">
  06_03</a> by sohnsookyoung (<a href="https://codepen.io/sohnsookyoung">@sohnsookyoung</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

```js
(function () {
  const stage = document.querySelector(".stage");

  function doorHandler(e) {
    //이벤트 객체 타겟 잡기
    const targetElem = e.target;

    // 활성화
    if (targetElem.classList.contains("door-body")) {
      targetElem.parentNode.classList.add("door-opened");
    }
  }
  stage.addEventListener("click", doorHandler);
})();
```

1. 전역 변수 사용을 하지 않기 위해서 처리
2. 이벤트 위임을 위해서 .stage를 우선 불러온다. => .stage에 이벤트 리스너 붙히기
3. doorHandler 메소드 작성
4. .stage 내에서 어떤 클래스가 클릭이 되었는지 알기 위해서 **e.target** 사용
5. .door:hover => .door-opened 클래스를 새로 만들어줌 => 그래서 만약 door-body 가 클릭된다면 .door-opened를 추가(classList.add('door-opened')) 해주기 위함
6. 클릭이 된 객체가 only .door-body 여야 하므로 예외처리를 해줌

## 4️⃣ 🌟활성화/비활성화

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="LYdYjBx" data-user="sohnsookyoung" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/sohnsookyoung/pen/LYdYjBx">
  06-04</a> by sohnsookyoung (<a href="https://codepen.io/sohnsookyoung">@sohnsookyoung</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

```js
(function () {
  const stage = document.querySelector(".stage");
  // 현재 활성화된 아이템을 저장하고 있는 변수
  let currentItem;

  function doorHandler(e) {
    //이벤트 객체 타겟 잡기
    const targetElem = e.target;

    const currentItem = document.querySelector(".door-opened");
    // 비활성화
    if (currentItem && targetElem.classList.contains("door-body")) {
      currentItem.classList.remove("door-opened");
    }
    // 활성화
    if (targetElem.classList.contains("door-body")) {
      targetElem.parentNode.classList.add("door-opened");
      currentItem = targetElem.parentNode;
    }
  }
  stage.addEventListener("click", doorHandler);
})();
```

dom을 직접 접근하는 것 보다는 함수 내의 전역 변수(currentItem)을 통해서 활성화, 비활성화를 조작할 수 있다.

- 활성화: 클릭이 되었다면 .door-opened 가 들어있는 노드를 currentItem 값으로 넣어준다.
- 비활성화: currentItem이 Null/undefined 가 아니라면 클래스가 remove 될 수 있도록 한다.

<br>

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="eYMYEaN" data-user="sohnsookyoung" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/sohnsookyoung/pen/eYMYEaN">
  06_05</a> by sohnsookyoung (<a href="https://codepen.io/sohnsookyoung">@sohnsookyoung</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

하지만 활성화 함수, 비활성화 함수를 각각 따로 만들어 주는 것이 좋다. 활성화 함수를 만들고 비활성화 함수를 만들어서 클릭이 되었을 때 doorHandler 가 작동이 되고 거기 안에서 조건문에 해당이 된다면 activate 함수 또는 inactivate 함수를 사용하도록 코드를 작성했다.
