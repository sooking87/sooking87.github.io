---
title: "[Section 01] Transform / Transition / Animation"
excerpt: "[Section 01] Transform / Transition / Animation"
categories: [Interactive Web]
tags: [Interactive Web, WEB]
toc: true
toc_sticky: true
---

## 🔮 Transform

### 📍 transform: scale( );

```html
<style>
  .box_container {
    display: flex;
  }
  .box {
    width: 100px;
    height: 100px;
    border: 2px solid black;
    background: rgba(255, 255, 0, 0.7);
  }
  .box:hover {
    transform: scale(2);
  }
</style>
```

- 중심을 기준으로 크기가 2개가 된다.

![download1](https://user-images.githubusercontent.com/96654391/169550001-1bb1350a-1bc4-4c22-8160-adc0db41f503.png)

<br>

```html
<style>
  .box_container {
    display: flex;
  }
  .box {
    width: 100px;
    height: 100px;
    border: 2px solid black;
    background: rgba(255, 255, 0, 0.7);
  }
  .box:hover {
    transform: scale(2) rotate(45deg);
  }
</style>
```

- 중심을 기준으로 크기가 2배가 되면서 45도 회전

![download1](https://user-images.githubusercontent.com/96654391/169550336-19789479-830b-4f97-a227-8999ddf8985e.png)

### 📍 transform: skew( );

```css
<style>
    .box_container {
        display: flex;
    }
    .box {
        width: 100px;
        height: 100px;
        border: 2px solid black;
        background: rgba(255, 255, 0, 0.7);
    }
    .box:hover {
        transform: skew(30deg);
    }
</style>
```

![download1](https://user-images.githubusercontent.com/96654391/169550653-89f830f5-2e62-4c0e-a6d3-de6ee332c3ac.png)

<br>

그외 skewX(), skewY() 도 있음.

### 📍 transform: translate(가로 px, 세로 px);

```css
<style>
    .box_container {
        display: flex;
    }
    .box {
        width: 100px;
        height: 100px;
        border: 2px solid black;
        background: rgba(255, 255, 0, 0.7);
    }
    .box:hover {
        transform: translate(30px, 10px); /* 왼쪽으로 30px, 오른쪽으로 10px*/
    }
</style>
```

- 가로px, 세로px 만큼 박스가 움직인다.

![download1](https://user-images.githubusercontent.com/96654391/169551093-56445bd6-f913-4b43-a92e-7e639994cede.png)

### 📍 기준점 바꾸기 : transform-origin 속성

- transform-origin: 좌우 상하;
- transform-origin: % %;

```css
<style>
    .box_container {
        display: flex;
    }
    .box {
        width: 100px;
        height: 100px;
        border: 2px solid black;
        background: rgba(255, 255, 0, 0.7);
    }
    .box:hover {
        /* 기준점 바꾸기 */
        transform: scale(1.5);
        transform-origin:left top; /* 왼쪽 위를 기준으로 박스가 2개가 된다. 가로 세로 */
    }
</style>
```

![download1](https://user-images.githubusercontent.com/96654391/169551497-7eac9d0a-bb37-46be-babf-60ce879aeca6.png) <br>

- 왼쪽 위를 기준으로 1.5배가 되었다.

## 🔮 Transition

transform 같은 경우는 변형 <br>
transition 같은 경우는 전환 / 애니메이션

### 📍 transition 속성

- transition-property : 적용 대상
- transition-duration : 몇 초 동안 적용
- transition-timing-function : 어떤 속도로 적용 될지 -> 검사에서 보라색 버튼 누르면 전환되는 속도를 원하는대로 만들 수 있다. -> 이거 복붙해서 코드에 넣으면 됨.
- transition-delay : 몇 초 뒤에 적용될지

```css
<style>
    .box_container {
        display: flex;
    }
    .box {
        width: 100px;
        height: 100px;
        border: 2px solid black;
        background: rgba(255, 255, 0, 0.7);
        transition: 0.5s;
    }
    .box:hover {
        width: 200px;
        background: red;
    }
</style>
```

![download1](https://user-images.githubusercontent.com/96654391/169556644-85f04087-afab-44fb-93e6-ec031ad19864.png) <br>

- 0.5초 동안 너비가 200, 색깔이 빨간색으로 전환됨

## 🔮 Animation

### 📍 사용법

```css
@keyframes sample-ani {
  0% {
    transform: translate(0, 0);
  }
  50% {
    transform: translate(300px, 0);
  }

  70% {
    transform: translate(400px, 500px);
  }
  100% {
    transform: translate(0, 0);
  }
}
```

이런식으로 만들어 주면 된다. 여기서 sample-ani 부분은 우리가 지정할 수 있는 것으로 애니메이션의 이름을 뜻한다.

<br>

0% ~ 100% 까지의 애니메이션일 때 (n-1)% ~ n%까지 중괄호 안에 있는 속성들이 적용이 된다.
-> 그리고 이렇게 정해놓은 애니메이션 이름을 적용할 클래스에 다음과 같이 넣어주면 된다.

```css
.box {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100px;
  height: 100px;
  border: 2px solid black;
  background: #fff000;
  animation: sample-ani 2s linear infinite;
}
```

- **_animation 속성_**
  - **animation-duration** : 몇 초 동안 적용
  - **animation-timing-function** : 어떤 속도로 적용 될지
  - **animation-delay** : 몇 초 뒤에 적용될지
  - **animation-iteration-count** : 반복 횟수(infinite / 숫자)
  - **animation-direction** : **alternative**(애니메이션이 0% -> 100% -> 0% 이런식으로 이동) / **reverse** (100% -> 0%)
  - **animation-fill-mode** (애니메이션이 끝났을 때 위치 조정(default: 0%에서의 위치로 돌아감)) : **forwards** (100%에서의 상태 그대로 남아있다.)
  - **animation-play-state** (애니메이션을 일시정지 할지 재생할지를 결정할 수 있다.): **running** (default) / **paused**
  - animation-name

### 📍 적용

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Interactive Web</title>
    <style>
      @keyframes spaceship-ani {
        100% {
          background-position: -2550px 0;
        }
      }
      .spaceship {
        width: 150px;
        height: 150px;
        background: url("../images/sprite_spaceship.png") no-repeat 0 0 / auto
          150px;
        animation: spaceship-ani 2s infinite steps(17);
      }
    </style>
  </head>
  <body>
    <div class="spaceship"></div>
  </body>
</html>
```

우선, sprite_spaceship.png 라는 이미지를 가져온다. <br>
![sprite_spaceship](https://user-images.githubusercontent.com/96654391/169565654-c8116371-e62f-41ef-9a6e-b22c2756cbde.png) <br>

이렇게 생김,,, 여튼 이거를 backgournd에 넣어 -> no-repeat에 -> 0 0 위치에서 시작 -> 크기를 auto 150px 만큼 잘라서 사용 <br>

그리고 애니메이션을 만들어서 `background-position: -2550px 0;` 로 애니메이션이 infinite되도록 만들어줌 -> 근데 왜 -2550px인지는 모르겠다. -> 사진을 잘보면 시작 부분부터 거꾸로 진행이 되어야 애니메이션처럼 진행됨

<br> <br>

최종 : div 태그안에 이미지 배경을 넣었는데, div 자체는 150 \* 150으로 만들었고, 불러온 배경은 0, 0에서부터 auto \* 150px씩 자르면서 진행됨 **_걍 개신기_**
