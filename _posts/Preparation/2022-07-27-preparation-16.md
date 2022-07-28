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
