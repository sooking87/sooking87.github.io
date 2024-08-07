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

### 🔆 .wall-right / .wall-left

양 옆에 있는 벽을 만들어주는 과정이다.

```css
.wall-left {
  left: -500vw;
  width: 1000vw;
  transform: rotateY(90deg);
}
.wall-right {
  left: -500vw;
  width: 1000vw;
  transform: rotateY(90deg) translateZ(100vw);
}
```

이걸 보면 일단 길이 자체를 원래 인사말이 적혀있는 wall 보다 10배정도는 길어야 되니까 1000vw 이고, y축 기준으로 돌리고 그런 다음 z축으로 100vw만큼 옯겨서 .wall-right를 옮긴다.

### 🔆 .wall-front-a / b / c / d

인사말이 적혀있는 벽에 입체감을 주기 위해서 적당한 위치에 translateZ를 통해서 옮겨준다.

```css
.wall-front-a {
  transform: translateZ(300vw);
}
.wall-front-b {
  transform: translateZ(50vw);
}
.wall-front-c {
  transform: translateZ(-200vw);
}
.wall-front-d {
  transform: translateZ(-500vw);
}
```

## 💎 js 작성

### 🔆 스크롤 할 때 앞으로 움직이게 하기

- pageYOffset: 문서에서 스크롤되고 있는 위치 / 전체 문서의 높이
- document.body.offsetHeight - window.innerHeight : 창 높이(스크롤 크기)
- pageYOffset / maxScrollValue : 스크롤되고 있는 비율

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="xxWqrVj" data-user="sohnsookyoung" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/sohnsookyoung/pen/xxWqrVj">
  11_03</a> by sohnsookyoung (<a href="https://codepen.io/sohnsookyoung">@sohnsookyoung</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

근데 여기서 문제는 위에 창 크기를 다르게 하면서 알 수 있겠지만 크기가 달라질 때마다 동작 화면이 다르게 나타난다.
=> 왜?: 화면 크기가 달라진다는 것은 document.body.offsetHeight가 바뀌기 때문이다.
=> sol?: resize 이벤트를 사용한다.

```js
function resizeHandler() {
  maxScrollValue = document.body.offsetHeight - window.innerHeight;
}
window.addEventListener("resize", resizeHandler);
resizeHandler();
```

창 사이즈가 바뀌어도 바뀐 창 사이즈 기준으로 적용이 되도록 한 것 이다.

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="RwMpgom" data-user="sohnsookyoung" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/sohnsookyoung/pen/RwMpgom">
  11-04</a> by sohnsookyoung (<a href="https://codepen.io/sohnsookyoung">@sohnsookyoung</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

### 🔆 화면 상단에 프로그래스바 만들기

```html
<div class="progress-bar-con">
  <div class="progress-bar"></div>
</div>
```

```css
.progress-bar-con {
  position: fixed;
  left: 0;
  top: 0;
  z-index: 100;
  width: 100vw;
  height: 5px;
  background: #555;
}
.progress-bar {
  width: 0;
  height: 5px;
  background: #00a8ff;
}
```

js를 통해서 스크롤 할 때마다 .progress-bar의 width를 수정하려고 한다.

```js
window.addEventListener(
  "scroll",
  function () {
    const scrollPar = pageYOffset / maxScrollValue;
    const zMove = scrollPar * 980 - 490;
    houseElem.style.transform = "translateZ(" + zMove + "vw)";

    // progressbar
    progressbarElem.style.width = scrollPar * 100 + "%";
  },
  false
);
```

아까 사용했던 scroll 이벤트 함수안에 코드 작성. 스크롤 관련된 이벤트니까!

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="oNqZwwm" data-user="sohnsookyoung" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/sohnsookyoung/pen/oNqZwwm">
  11-05</a> by sohnsookyoung (<a href="https://codepen.io/sohnsookyoung">@sohnsookyoung</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

### 🔆 마우스 위치에 따라서 시점 다르게 하기

워우어우어우어우ㅜ 대박 신기!

- mousemove 이벤트 사용
- e.clientX: 마우스의 x 좌표
- e.clientY: 마우스의 y 좌표

근데 원하는 거는 가운데를 기준으로 왼쪽으로 갈수록 x 좌표는 -1로, 오른쪽으로 갈수록 1로 좌표를 수정하고 싶다.
=> sol. mousePos 객체를 마우스의 x좌표와 y좌표를 수정해준다.

```js
const mousePos = {
  x: 0,
  y: 0,
};
mousePos.x = -1 + (e.clientX / this.window.innerWidth) * 2;
mousePos.y = 1 - (e.clientY / this.window.innerHeight) * 2;
```

이렇게 된다면 가운데가 0을 기준으로 x 좌표 기준 왼쪽으로 가면 -1, 오른쪽으로 가면 +1, y 좌표 기준으로 위쪽으로 가면 +1, 아래로 가면 -1로 된다.

이런 상태로 rotateX, rotateY를 사용해서 시점이 바뀌도록 바꾸어 주어야 한다.
근데 여기서 rotateX를 사용하게 되면 ----이 축을 기준으로 움직이는 것이니까 y 좌표와 관련이 있고, rotateY를 사용하게 되면 | 이 축을 기준으로 움직이게 되는 것이니까 x 좌표와 관련이 있다.

```js
stageElem.style.transform =
  "rotateX(" + mousePos.y * 5 + "deg) rotateY(" + mousePos.x * 5 + "deg)";
```

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="OJvpjZz" data-user="sohnsookyoung" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/sohnsookyoung/pen/OJvpjZz">
  11-06</a> by sohnsookyoung (<a href="https://codepen.io/sohnsookyoung">@sohnsookyoung</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

개신기함 ㅇㅇ

## 💎 character

### 🔆 일단 Character 생성자 만들기

Character.js의 경우는 생성자이기 때문에 파일의 첫 글자를 대문자로 넣은 것이다.
이 생성자를 통해서 `new Character();` 을 통해서 계속 일분이를 넣어줄 예정인 것 같다.

```js
// Character.js
function Character() {
  this.mainElem = document.createElement("div");
  this.mainElem.classList.add("character");
  this.mainElem.innerHTML =
    "" +
    '<div class="character-face-con character-head">' +
    '<div class="character-face character-head-face face-front"></div>' +
    '<div class="character-face character-head-face face-back"></div>' +
    "</div>" +
    '<div class="character-face-con character-torso">' +
    '<div class="character-face character-torso-face face-front"></div>' +
    '<div class="character-face character-torso-face face-back"></div>' +
    "</div>" +
    '<div class="character-face-con character-arm character-arm-right">' +
    '<div class="character-face character-arm-face face-front"></div>' +
    '<div class="character-face character-arm-face face-back"></div>' +
    "</div>" +
    '<div class="character-face-con character-arm character-arm-left">' +
    '<div class="character-face character-arm-face face-front"></div>' +
    '<div class="character-face character-arm-face face-back"></div>' +
    "</div>" +
    '<div class="character-face-con character-leg character-leg-right">' +
    '<div class="character-face character-leg-face face-front"></div>' +
    '<div class="character-face character-leg-face face-back"></div>' +
    "</div>" +
    '<div class="character-face-con character-leg character-leg-left">' +
    '<div class="character-face character-leg-face face-front"></div>' +
    '<div class="character-face character-leg-face face-back"></div>' +
    "</div>";

  document.querySelector(".stage").appendChild(this.mainElem);
}
```

HTML을 js로 넣는 과정 Elem을 하나 만들고, 거기에 넣을 css를 넣어주고, innerHTML을 통해서 만들어준다. 그리고 그 만들어준 Elem을 어디에 넣어야되는지 확인해보고 appendChild를 통해서 넣어준다.

### 🔆 클릭했을 때 해당 위치에 캐릭터 생성하기

```js
// wall3d.js
stageElem.addEventListener("click", function (e) {
  new Character({
    xPos: (e.clientX / window.innerWidth) * 100,
  });
  // console.log(e.clientX / this.windowWidth) * 100;
});
```

해당 위치에 비율을 계산해서 Character 생성자로 전달

```js
// Character.js
this.mainElem.style.left = info.xPos + "%";
```

### 🔆 스크롤 했을 때 앞으로 가고 뒤로 가고

그러기 위해서는 우선
스크롤을 할 때 팔다리 움직이고 스크롤 안하면 팔다리 멈추게 하는 것 부터 해본다.

```js
// Character.js
...

  // 스크롤 중인지 아닌지
  this.scrollState = false;

...
Character.prototype = {
  constructor: Character,
  init: function () {
    const self = this;
    window.addEventListener("scroll", function () {
      this.clearTimeout(self.scrollState);

      if (!self.scrollState) {
        self.mainElem.classList.add("running");
      }

      self.scrollState = setTimeout(function () {
        self.scrollState = false;
        self.mainElem.classList.remove("running");
      }, 500);
    });
  },
};
```

객체 생성 -> scrollState = false 인 상태, 동시에 if 문 통과(running 클래스 생성) -> 스크롤 중(scrollState = True) -> clearTimeout 적용 동시에 밑에 setTimeout 부분은 실행 X(정확히 왜,,,,?) -> 스크롤 정지(scrollState = false) -> setTimeout 실행

### 🔆 스크롤 내리면 뒷모습, 올리면 앞모습

codePen에 파일 두개를 넣는 방법을 몰라서 너무 아쉽지만! 그냥 코드로 작성해본다면 필요한 요소는 우선 스크롤 위치와 이전 스크롤 위치가 필요하다.

```js
...

  // 바로 이전 스크롤 위치
  this.lastScrollTop = 0;

...

Character.prototype = {
  constructor: Character,
  init: function () {
    const self = this;
    window.addEventListener("scroll", function () {
      this.clearTimeout(self.scrollState);

      if (!self.scrollState) {
        self.mainElem.classList.add("running");
      }

      self.scrollState = setTimeout(function () {
        self.scrollState = false;
        self.mainElem.classList.remove("running");
      }, 500);

      // 이전 스크롤 위치와 현재 스크롤 위치를 비교
      if (self.lastScrollTop > pageYOffset) {
        // 스크롤 올림
        self.mainElem.setAttribute("data-direction", "backward");
      } else {
        // 스크롤 내림
        self.mainElem.setAttribute("data-direction", "forward");
      }
      // pageYOfset: 스크롤 위치 가져오기
      // lastScrollTop: 바로 이전 스크롤 위치
      self.lastScrollTop = pageYOffset;
    });
  },
}
```

- pageYOffset: 스크롤 위치 가져오기
- lastScrollTop: 바로 이전 스크롤 위치
- 캐릭터 객체에 setAttribute를 통해서 css 속성 적용

### 🔆 좌우로 이동하기

먼저 방향키를 통해서 움직일 수 있도록 하기 위해서 keydown, keyup 이벤트를 작성한다.

```js
window.addEventListener("keydown", function (e) {
  // 37: 왼쪽, 39: 오른쪽
  if (e.keyCode === 37) {
    self.mainElem.setAttribute("data-direction", "left");
    self.mainElem.classList.add("running");
  } else if (e.keyCode === 39) {
    self.mainElem.setAttribute("data-direction", "right");
    self.mainElem.classList.add("running");
  }
});

window.addEventListener("keyup", function (e) {
  self.mainElem.classList.remove("running");
});
```

그런 다음에 방향키 방향대로 움직일 수 있도록 한다. => HOW? <br>
<br>

보면은 1초에 10번 즉, 1초에 10프레임정도가 출력이 되는데, 일반적으로 영상처럼 보이기 위해서는 20~30프레임 정도가 필요하다고 한다. 그래서 이를 위해서는 **_requestAnimationFrame_** 을 사용하면 된다.

```js
  run: function (self) {
    if (self.direction === "left") {
      self.xPos -= self.speed;
    } else if (self.direction === "right") {
      self.xPos += self.speed;
    }

    if (self.xPos < 2) {
      self.xPos = 2;
    } else if (self.xPos > 88) {
      self.xPos = 88;
    }
    self.mainElem.style.left = self.xPos + "%";
    requestAnimationFrame(function () {
      self.run(self);
    });
```

프로토타입에 run이라는 메소드 추가
zzzzzzzzzzㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋ개어렵눜ㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋ하
여튼 포인트는 runningState를 사용해서 움직였다가 안움직였다가 requestAnimationFrame을 했다가 cancelAnimationFrame을 했다가 ㅇㅇ

```js

...

  // 좌우 이동 중인지 아닌지
  this.runnintState = false;
  this.rafId;

...

window.addEventListener("keydown", function (e) {
      if (self.runningState) return;
      // 37: 왼쪽, 39: 오른쪽
      if (e.keyCode === 37) {
        self.direction = "left";
        self.mainElem.setAttribute("data-direction", "left");
        self.mainElem.classList.add("running");
        self.run(self);
        self.runningState = true;
      } else if (e.keyCode === 39) {
        self.direction = "right";
        self.mainElem.setAttribute("data-direction", "right");
        self.mainElem.classList.add("running");
        self.xPos += self.speed;
        self.run(self);
        self.runningState = true;
      }
    });
    window.addEventListener("keyup", function (e) {
      self.mainElem.classList.remove("running");
      this.cancelAnimationFrame(self.rafId);
      self.runningState = false;
    });
  },
  run: function (self) {
    if (self.direction === "left") {
      self.xPos -= self.speed;
    } else if (self.direction === "right") {
      self.xPos += self.speed;
    }

    if (self.xPos < 2) {
      self.xPos = 2;
    } else if (self.xPos > 88) {
      self.xPos = 88;
    }
    self.mainElem.style.left = self.xPos + "%";
    self.rafId = requestAnimationFrame(function () {
      self.run(self);
    });
  },
```

### 🔆 속도 차이 만들기

character 객체로 전달되는 info에 speed 라는 속성 추가

```js
// wall3d.jd
stageElem.addEventListener("click", function (e) {
  new Character({
    xPos: (e.clientX / window.innerWidth) * 100,
    speed: Math.random(),
  });
  // console.log(e.clientX / this.windowWidth) * 100;
});
```

## 💎 테마 바꾸기

= 이벤트 위임

```js

...

const selectCharacterElem = document.querySelector(".select-character");

...

  selectCharacterElem.addEventListener("click", function (e) {
    const value = e.target.getAttribute("data-char");
    document.body.setAttribute("data-char", value);
  });
```
