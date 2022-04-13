---
title: "[생활 코딩] React 사용 방법"
excerpt: "[생활 코딩] React 사용 방법"
categories: [생활 코딩]
tags: [생활 코딩, WEB]
toc: true
toc_sticky: true
---

## js 코딩 하는 법

리액트를 통해서 폴더를 만들게 되면 크게 `public`폴더와 `src`폴더가 있다. 먼저 `public > index.html`파일을 보게 되면 id="root"를 통해서 작동함을 알 수 있다. 이 root는 `src > index.js`와 관련있음을 알 수 있다.

<iframe src="https://codesandbox.io/embed/winter-shape-9yl42?fontsize=14&hidenavigation=1&theme=dark&view=editor"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="winter-shape-9yl42"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

그리고 `src > App.js`파일을 보니 function 형태로 되어 있지만 클래스를 사용해 주기 위해서 `class App extends Component`로 수정해 주었다. 그리고 js와 관련된 내용을 넣기 위해서는 return 안에 있는 div 태그 안에 내용을 추가해주면 된다.

<iframe src="https://codesandbox.io/embed/winter-shape-9yl42?fontsize=14&hidenavigation=1&theme=dark&view=editor"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="winter-shape-9yl42"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>


## css 코딩 하는 법

css를 코딩하는 법은 간단하다. 그냥 .css 확장자 파일을 만들어주고, 내용을 적는다. 그 다음 이에 해당하는 .js파일에 임포트만 해주면 된다.
