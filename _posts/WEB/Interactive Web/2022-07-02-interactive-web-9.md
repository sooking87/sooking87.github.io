---
title: "[Section 07] 객체"
excerpt: "[Section 07] 객체"
categories: [Interactive Web]
tags: [Interactive Web, WEB]
toc: true
toc_sticky: true
---

## 🔮 객체 1

객체를 생성하는 방법

```js
const person = {};
// 속성, property :
person.name = "일분이";
person.age = 10;
person.introduce = function () {
  console.log("안녕하세요. 저는 일분이 이고 나이는 10살이에요.");
};
person.introduce();

const person2 = {
  name: "일분이",
  age: 10,
  introduceMySelf: function () {
    console.log("안녕?");
  },
};
person2.introduceMySelf();
```

## 🔮 객체 2

this.

```js
const person = {
  name: '일분이', 
  age: 10,
  introduce: function() {
      console.log("안녕하세요. 저는 " + this.name + "이고, 나이는 " + this.age + "살이에요.");
  },
};

const person2 = {
  name: '이분이', 
  age: 8,
  introduce: function() {
      console.log("안녕하세요. 저는 " + this.name + "이고, 나이는 " + this.age + "살이에요.");
  },
};
person.introduce();
person2.introduce();
```

## 🔮 객체 3

생성자 만들기 => 함수를 통해서 객체를 생성해 주는 함수, 이 함수의 경우에는 첫 문자를 대문자로 해줍니다. <br>

- new: 새로운 객체를 만들어 주는 예약어
- 인스턴스: 객체를 만드는 함수를 통해서 만들어준 객체 하나를 부르는 말

```js
// 구조는 같되, 안에 속성값이 다른 객체를 만드는 방법
// 객체를 생성해주는 함수는 첫 문자를 대문자로 해준다. 
function Person(name, age) {
    this.name = name;
    this.age = age;
    this.introduce = function () {
        console.log("안녕하세요. 저는 " + this.name + "이고, 나이는 " + this.age + "살이에요.");
    };
}

const person1 = new Person("일분이", 10);
const person2 = new Person("이분이", 8);

person1.introduce();
person2.introduce();
```

## 🔮 객체 4

function introduce와 같은 메소드는 모든 객체가 공유해서 가능하다. 하지만 각 객체별로 별도의 공통 메소드를 넣는 것은 메모리상 낭비이다. 따라서 prototype 안에 메소드를 넣어주면 객체당 introduce 메소드를 공유할 수 있도록 한다. <br>

🔹 정리 <br>
- 변하는 속성: 객체 안에 넣어주기
- 변하지 않은 공통 속성: 생성자 함수.prototype.메소드 를 사용하기

### 📍 활용 - 카드 만들기

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="rNdVjZp" data-user="sohnsookyoung" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/sohnsookyoung/pen/rNdVjZp">
  07</a> by sohnsookyoung (<a href="https://codepen.io/sohnsookyoung">@sohnsookyoung</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

Card라는 생성자에는 숫자와 색깔이 변하고 카드의 모양과 글씨체 등은 동일하게 해야된다. 

- 숫자와 색깔은 변하는 값이므로 
  ```js
  function Card(num, color) {
      this.num = num;
      this.color = color;
      this.init();
  }
  ```

- 카드의 모양은 변하지 않으므로 
  ```js
  Card.prototype = {
      constructor: Card,
      init: function() {
          const mainElem = document.createElement('div');
          mainElem.style.color =  this.color;
          mainElem.innerHTML = this.num;
          mainElem.classList.add('card');
          document.body.appendChild(mainElem);
      }
  }
  ```

  카드 div 생성하는 방법
  1. div라는 태그를 생성(createElement)해 준다. 
  2. 카드의 숫자와 색깔을 생성자의 속성값을 통해서 만들어준다. 
  3. div 태그 안에 지정해둔 card 클래스 스타일을 적용시킨다. (classList.add('card'))
  4. body 태그에 요소를 넣어준다. 