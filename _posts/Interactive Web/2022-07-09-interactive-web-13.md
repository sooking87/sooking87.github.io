---
title: "[Section 11] 전진! 3D 스크롤"
excerpt: "[Section 11] 전진! 3D 스크롤"
categories: [Interactive Web]
tags: [Interactive Web, WEB]
toc: true
toc_sticky: true
---

## 💎 (뇌피셜) 프론트 프로젝트 하려면 정해야되는 것

1. 일단은 디자인을 그릴 거 아니야
2. 그걸 그리면 각 요소별로 class를 회의해 -> 이때 비슷한 요소의 경우는 최대한 클래스를 분류하고 마지막에는 고유 클래스까지 지정
3. 2번이랑 같이 진행해야되나? 여튼 html 파일 작성 = 구성 작성
   ```html
   <div class="world">
     <div class="stage">
       <div class="house">
         <section class="wall wall-left"></section>
         <section class="wall wall-right"></section>
         <section class="wall wall-front wall-front-a">
           <div class="wall-content">
             <h2 class="wall-title">안녕하세요</h2>
           </div>
         </section>
         <section class="wall wall-front wall-front-b">
           <div class="wall-content">
             <h2 class="wall-title">Hello</h2>
           </div>
         </section>
         <section class="wall wall-front wall-front-c">
           <div class="wall-content">
             <h2 class="wall-title">Hola</h2>
           </div>
         </section>
         <section class="wall wall-front wall-front-d">
           <div class="wall-content">
             <h2 class="wall-title">こんにちは</h2>
           </div>
         </section>
       </div>
     </div>
   </div>
   ```
4. css 작성

## 💎 css 작성

### 🔆 .world 작성

- world에 3D 공간을 넣어주어야 한다. = `perspective: 1000px;`
- 스크롤을 내리면 화면이 아래로 내려가는 것이 아니라 앞뒤로 3D 공간처럼 움직여야 된다. 즉, **world 라는 공간은 현재 화면에 고정되어 있어야 한다.**
  ```css
  position: fixed;
  left: 0;
  top: 0;
  width: 100vw;
  height: 100vh;
  ```
  뷰포트 단위가 가장 확실하게 화면에 의도대로 움직일 수 있다.

### 🔆 .stage 작성

- .stage가 있는 이유: 이거는 확실히 직접 html을 작성해봐야 뼈져리게 느끼겠지만! 여튼 지금 버튼을 클릭하면 캐릭터가 생기는데 인사말이 들어있는 벽과 캐릭터를 같이 감싸고 있는 클래스가 필요하다.
- `transform-style: preserve-3d;` : .world에서 만든 3D 공간을 상속(?) 시켜주어서 최종 자식에게까지 3D perspective가 전달되도록 하기 위해서.

### 🔆 .wall 작성

어떤 식으로 저런 3D 벽을 만들꺼냐면

1. 일단 6개의 벽(글씨가 적혀있는 벽 4개, right, left 각각 1개)을 absolute를 통해서 겹쳐
2. 그리고 아직 z 축을 설정을 안해준거니까 제일 마지막 요소가 위쪽으로 올라와있다.

```css
.wall {
  width: 100vw;
  height: 100vh;
  background: rgba(255, 255, 255, 0.8);
  position: absolute;
  left: 0;
  top: 0;
}
```

그리고 벽에 써져있는 글씨체나 정렬 바꾸어주기.

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="dymMBqz" data-user="sohnsookyoung" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/sohnsookyoung/pen/dymMBqz">
  11_01</a> by sohnsookyoung (<a href="https://codepen.io/sohnsookyoung">@sohnsookyoung</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>
<br>

그럼 이런 상태!

[--temp--] 4 강의 마무리
