---
title: "[WEB] Emotion-Diary / Mini-Waterglass"
excerpt: "[WEB] Emotion-Diary / Mini-Waterglass"
categories: [Preparation]
tags: [Preparation, WEB, React]
toc: true
toc_sticky: true
---

## 목표

1. textarea -> 마크다운 형식으로
2. Dark/Light Mode
3. 글씨체 수정
4. DiaryItem -> 캘린더에 넣기

## MarkDown API

- <https://github.com/komagata/textarea-markdown>
- <https://www.npmjs.com/package/textarea-markdown-editor/v/0.1.12>
- <https://codesandbox.io/s/1r3bk?file=/src/MarkdownEditor.jsx>
- <https://codesandbox.io/s/v8x96ppjj7?file=/src/index.js> => 코드 샌박에 코드가 있는데 나만 안돼,,? <br>
  <br>

**_👌 이거는 코드샌박에서 적용되는 거_** <br>

<https://codesandbox.io/s/g0hif> <br>
<https://codesandbox.io/s/markdown-previewer-ri87w?file=/src/App.js>

## Markdown-it

<https://codesandbox.io/s/markdown-previewer-ri87w?file=/src/App.js> <br>

해당 코드에 나와있는 깃헙 README.md에 잘 나와있다. 모듈들을 다 다운받아야 된다는 점,,,<br>
<https://github.com/markdown-it/markdown-it>
<br>

여튼 여기서 코드 가져와서 TextArea 컴포, MarkdownEditor 컴포, Preview 컴포를 따로 만들어서 사용하였다.
<br>

자세한 내용은 깃헙에서!
<br>
<https://github.com/sm-CODE-IT/Mini_Waterglass/tree/main>

## 글씨체 수정

나눔 명조체, 나눔 손글씨체로 함.
<br>

```css
@import url("https://fonts.googleapis.com/css2?family=Nanum+Myeongjo&family=Nanum+Pen+Script&display=swap");
```

## Light/Dark Mode

- <https://velog.io/@elinapark/Styled-Components> => styled-components 모듈을 사용하는 방법이 잘 나와있음!
- <https://xtring-dev.tistory.com/entry/Styling-Styled-Components-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B3%A0-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0-%F0%9F%92%85> => 리액트에서 styled-component를 사용하는 이유와 사용법이 상세히 나와있음
- <https://medium.com/hackernoon/5-ways-to-animate-a-reactjs-app-in-2019-56eb9af6e3bf> -> 리액트에서 애니메이션 및 transform, transition을 적용시킬 수 있는 방법
- <https://dbramwell.github.io/react-animate-on-scroll/#animateIn> => 다양한 styled-components의 애니메이션이 소개되어 있는 곳: 나중에 프젝할 때 사용할 수 있을 듯
  - 해당 깃헙: <https://github.com/dbramwell/react-animate-on-scroll>
- <https://www.framer.com/motion/> => 헐 미친 리액트 애니메이션 관련 모듈,,,

## 🌟 적용해보기

<https://www.framer.com/motion/> <br>
<https://velog.io/@deli-ght/%EC%8A%A4%EB%8D%B0%EB%B8%8C-%EA%B0%9C%EB%B0%9C-%EC%9D%BC%EC%A7%80-4> -> tsx 너 뭔데?!(Dark/Light ver)

## DiaryItem -> 캘린더에 넣기

- <https://u-it.tistory.com/entry/FullCalendar-%EC%9D%B4%EB%B2%A4%ED%8A%B8-%EC%98%B5%EC%85%98-%EC%86%8D%EC%84%B1-%EB%8F%99%EC%A0%81%EC%A0%91%EA%B7%BC-MonthList-%EB%8F%99%EC%9D%BC%EC%A0%81%EC%9A%A9-%EC%83%89%EC%83%81-%EB%B3%80%EA%B2%BD>
- <https://vmar76.medium.com/how-to-create-an-event-in-the-fullcalendar-library-eaac8679e90> : json으로 addEvent
- <https://stackoverflow.com/questions/23872898/set-events-in-fullcalendar-from-array> : 배열로 동적 추가
- <https://codepen.io/pen?&editors=001> : 관련 코드팬 자료 근데 얘는 jQuery 사용,,,,
  <br> <br>

- <https://velog.io/@devyang97/FullCalendar-v5-Date-Clicking-Selecting> -> 여차저차 하면 되지 않을까,,?
- <https://codesandbox.io/s/fullcalendarreactrenderevent-t9d75?file=/src/FullCalendar.js> -> fullCalendar API를 객체로 사용하는 방법

## mouse over in FullCalendar

- <https://codepen.io/IsmiKin/pen/WbOeGw> : popover
