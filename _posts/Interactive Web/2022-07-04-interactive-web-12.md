---
title: "[Section 10] 타이밍 제어하기"
excerpt: "[Section 10] 타이밍 제어하기"
categories: [Interactive Web]
tags: [Interactive Web, WEB]
toc: true
toc_sticky: true
---

## 🔮 setTimeout

***setTimeout(function(){}, --(ms))*** 의 형식으로 사용이 되며, 리턴값으로는 숫자이다. 
```js
function sample() {
    console.log("sample!");
}

// 리턴값은 실행 숫자.
timeId = setTimeout(sample, 3000);
console.log(timeId);
```

<br>

***clearTimeout*** 은 setTimeout을 취소시켜버리는 기능을 가지고 있다. 
<br> 
그래서 취소 버튼을 만들어서 취소 버튼을 클릭하면 clearTimeout이 적용되도록 할 수 있다. 

```js
let timeId;
const btn = document.querySelector('.btn');

function sample() {
    console.log("sample!");
}

// 리턴값은 실행 숫자.
timeId = setTimeout(sample, 3000);
console.log(timeId);

btn.addEventListener("click", function() {
    clearTimeout(timeId); // setTimeout을 취소해버린다. 
})
```

## 🔮 setInterval

***setInterval(function(){}, ms)*** 의 형식으로 사용이 되며 ms 후에 function 수행을 해주며, 끊임없이 반복이 된다. <br>

```js
let timeId;
const btn = document.querySelector('.btn');

function sample() {
    console.log("sample!");
}

// 리턴값은 실행 숫자.
timeId = setInterval(sample, 100);
console.log(timeId);

btn.addEventListener("click", function() {
    clearTimeout(timeId); // setTimeout을 취소해버린다. 
})
```

똑같이 setInterval은 clearInterval을 가지고 있다. setInterval을 멈추게 한다. 즉 위 코드로 따지면 버튼을 클릭하면 setInterval이 멈추게 된다. 

## 🔮 requestAnimationFrame

setInterval과 유사하지만 기능상 requestAnimationFrame이 더 우세하므로 요즘은 requestAnimationFrame을 사용하는 비중이 크다. 
<br>

requestAnimationFrame은 사용하려는 함수 안에 넣어주어서 사용을 한다. 반복을 멈추기 위해서는 ***cancelAnimationFrame*** 을 사용해준다. 

```js
let timeId;
const btn = document.querySelector('.btn');

function sample() {
    console.log("sample!");

    timeId = requestAnimationFrame(sample);
}

sample();

btn.addEventListener("click", function() {
    cancelAnimationFrame(timeId); 
})
```