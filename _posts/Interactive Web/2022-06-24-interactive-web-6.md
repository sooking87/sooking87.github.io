---
title: "[Section 04] 인터랙티브 웹 개발을 위한 자바스크립트"
excerpt: "[Section 04] 인터랙티브 웹 개발을 위한 자바스크립트"
categories: [Interactive Web]
tags: [Interactive Web, WEB]
toc: true
toc_sticky: true
---

## 🔮 자바스크립트 워밍업

기존 익스플로러 11에서 지원하는 것을 배우기 위해서 변수 이름을 var이 아닌 let 또는 const로 사용해줄 예정. <br>

그리고 같은 코드에서 var과 let을 동시에 사용하는 것은 안좋은 코드이다. <br>

- var: 변수의 유효 범위는 함수 내에서만 적용되도록 한다.
- let, const: 변수의 유효 범위는 중괄호 블록 안에서만 해당한다.

```js
if (true) {
    var a = 100;
}
console.log(a);

>>> 100
```

var의 경우에는 함수 단위로 scope가 결정이 되므로 if 문은 그냥 바깥에 있는 것과 같이 볼 수 있다.

```js
if (true) {
    let a = 100;
}
console.log(a);

>>> err
```

let 경우는 {} 단위이므로 에러가 난다.

## 🔮 DOM 스크립트 1

DOM: Document Object Model

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="WNMVRKK" data-user="sohnsookyoung" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/sohnsookyoung/pen/WNMVRKK">
  Untitled</a> by sohnsookyoung (<a href="https://codepen.io/sohnsookyoung">@sohnsookyoung</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

일단 이런식으로 웹 페이지를 잡아놓는다.

```js
const il = document.querySelector('.a');
undefined
il

>>>
<div class=​"ilbuni a">​…​</div>​
```

하나의 dom을 조정하기 위해서는 .Class 를 사용해준다.

```js
onst all = document.querySelectorAll('.ilbuni');
undefined
all
all[2]


>>>
NodeList(4) [div.ilbuni.a, div.ilbuni.b, div.ilbuni.c, div.ilbuni.d]
0: div.ilbuni.a
1: div.ilbuni.b
2: div.ilbuni.c
3: div.ilbuni.d
length: 4
[[Prototype]]: NodeList

<div class=​"ilbuni c">​…​</div>​<img src=​"../​images/​ilbuni_2.png" alt=​"ilbuni c">​</div>​
```

.ilbuni를 클래스로 가지고 있는 4개의 dom을 조작하기 위해서는 **_querySelectorAll('.class');_** 를 사용해준다.

## 🔮 DOM 스크립트 2

### 📍 setAttribute(), getAttribute()

```js
const char = document.querySelector('.characters');
>>> undefined
char
>>> <div class=​"characters">​…​</div>​ flex

char.setAttribute('data-id', 123);
```

이렇게 해주면 .characters의 id를 123으로 동적으로 추가된 것을 확인할 수 있다.

- data-index
- data-id
- data-role
  <br>

등 data-의 형식으로 시작하면 어떤 속성이든 필요에 따라 임의로 값을 추가할 수 있다.

## 🔮 DOM 스크립트 3

각 item 들을 조립해보는 것을 할 예정이다.

### 📍 새로 item 만들기

```js
const pElem = document.createElement('p')
pElem
>>> <p>​</p>​
pElem.innerHTML = '안녕?'
pElem
>>> <p>​안녕?​</p>​
const char = document.querySelector('.characters');
char.appendChild(pElem)​
```

1. createElement('p')를 통해서 새로운 p 태그를 만들어 준다.(**_createElement('p')_** )
2. innerHTML을 통해서 p 태그 안에 넣어줄 값을 넣어준다.(**_innerHTML_** )
3. appendChild를 통해서 .characters 안에 마지막 자식으로 p 태그를 추가해준다.(**_appendChild_** )

### 📍 두 번째 요소 지우기

```js
char.removeChild(document.querySelector(".b"));
```

두 번째 일분이가 없어진 것을 확인할 수 있다.

### 📍 클래스 요소에 새로운 클래스 추가하기

css에 special 클래스에 대한 스타일을 적어준다.
그 후 js를 통해서 첫 번째 일분이에 special 클래스를 넣어주어서 스타일을 적용시켜본다.

```js
ilbuni.classList.add("special");
```

이렇게 클래스 리스트에 special 클래스를 추가시켜주면 다음과 같이 스타일링이 적용됨을 알 수 있다. <br>
![download1](https://user-images.githubusercontent.com/96654391/175479908-3ebcf7f3-54b9-412f-b8c3-d66cc4786676.png) <br>

### 📍 클래스 삭제하기

```js
ilbuni.classList.remove("ilbuni");
```

클래스 ilbuni를 지우게 된다면 기존에 ilbuni를 통해서 적용되었던 스타일이 적용되지 않을 것이다. <br>

![download2](https://user-images.githubusercontent.com/96654391/175480658-eec05276-db41-44aa-9703-5d80e1ead257.png) <br>

### 📍 클래스 붙혔다 뗐다 하기

```js
ilbuni.classList.toggle("ilbuni");
// ilbuni 클래스 생김
ilbuni.classList.toggle("ilbuni");
// ilbuni 클래스 사라짐
```
