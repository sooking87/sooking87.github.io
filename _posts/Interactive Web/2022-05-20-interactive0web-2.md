---
title: "[Section 02] CSS 3D #1"
excerpt: "[Section 02] CSS 3D #1"
categories: [Interactive Web]
tags: [Interactive Web, WEB]
toc: true
toc_sticky: true
---

# CSS 3D

## 🔮 CSS 3D #1

예를 들어서 카드에 3D를 적용시키고 싶다면 그 카드가 있는 공간 자체를 3D로 만들어야 된다. -> **_perspective: px;_**

### 📍 .html

```html
<body>
  <div class="world">
    <div class="card">CARD</div>
    <div class="card">CARD</div>
    <div class="card">CARD</div>
  </div>
</body>
```

### 📍 .css

```html
<style>
  .world {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 80vw;
    height: 60vh;
    background: #fff000;
    perspective: 500px;
  }
  .card {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100px;
    height: 150px;
    border-radius: 0.5em;
    font-size: 1.5rem;
    margin: 1em;
    background: red;
    transform: rotateY(45deg);
  }
</style>
```

- rem: html의 font-size 기준으로 크기를 조정
- em: font-size 기준의 상대적 크기 -> 그래서 font-size를 키우면 border-radius도 커지고, font-size가 작아지면 border-radius도 작아진다.
- rotateY(45deg) : y축 기준으로 45도 돌리는데, 그 주변 공간을 3D로 만들어 주어야 원하는대로 나옴
- perspective: 500px; : 3D로 만드는 방법 -> 옆에 숫자는 얼마나 내 눈에서 멀리 있는 시점으로 볼 것이냐를 뜻함
  <br>

![download1](https://user-images.githubusercontent.com/96654391/169619816-196016e2-b302-4844-ac00-4ca618566d2f.png)

<br>
하지만 이 사진을 보면 세 개의 카드 모양이 조금씩 다르다는 것을 알 수 있다. -> 모두 같은 모양으로 돌아갈 수 있도록 하는 방법?
<br>

sol. card 클래스에 3D를 넣어주면 됨.

```css
.card {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100px;
  height: 150px;
  border-radius: 0.5em;
  font-size: 1.5rem;
  margin: 1em; /*
rem : html의 font-size 기준의 상대적 크기 em : font-size 기준의 상대적 크기 */
  background: red;
  transform: perspective(500px) rotateY(45deg);
}
```

![download2](https://user-images.githubusercontent.com/96654391/169642265-1a7db63a-c05a-4afa-a324-b5360be3574e.png)
