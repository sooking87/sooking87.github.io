---
title: "[WEB] MoonCalendar"
excerpt: "[WEB] MoonCalendar"
categories: [Preparation]
tags: [Preparation, WEB, React]
toc: true
toc_sticky: true
---

## 동적으로 input 태그 추가

- <https://codesandbox.io/s/practical-lake-yw22u?from-embed=&file=/src/App.js> : Suspense 태그 사용
- <https://www.thecodeteacher.com/question/115409/reactjs---How-to-use-%60React.createElement%60-children-parameter-(without-jsx)> : createElement 사용
- <https://blog.bitsrc.io/top-5-rich-text-editors-for-react-in-2021-628fecf0f7e0> : 직접 만드는 것 보다는 React Editor를 사용하는게 좋을까?
- <https://draftjs.org/docs/getting-started> : draft.js
- <https://codesandbox.io/s/g6lxrz>, <https://www.telerik.com/kendo-react-ui/components/editor/> : KendoReact Editor
- <https://codesandbox.io/s/0p6zjoy7x0?file=/index.js:0-1788> : 원하는 형식대로 Draft.js 사용한 코드 샌박 발견!
- <https://blog.logrocket.com/building-rich-text-editors-in-react-using-draft-js-and-react-draft-wysiwyg/> : Draft.js에서 사용된 Rich Text에 대한 자세한 설명
- <https://bigbite.net/2017/12/13/building-editor-draft-js-react/> : get HTML from Draft.js
- <https://github.com/sstur/draft-js-utils> : HTML을 불러오기 위해서 draft-convert가 버젼상 사용이 안되므로 해당 링크게 export-html, import-html 모듈을 사용

<br>
<br>

EditDiary > EditContainer 인 경우 이렇게 코드 쓰면 실행은 됨,

근데 문제는 컴포넌트를 나눠서 하면서 동시에 EditDiary에서 html로 바뀐 str을 받고 싶은 것,, 그럴려면 어떻게 해야되나,,,,,,,

### onEdit 시 기존 텍스트 나오게 하기

- <https://github.com/facebook/draft-js/issues/284> : sol 1
- <https://github.com/HubSpot/draft-extend>
- <https://bestofreactjs.com/repo/jpuri-react-draft-wysiwyg-react-rich-text-editing>
  문제점 1: 기존의 draft.js의 Editor와 wysiwyg의 Editor와는 차이가 있다. 누군가가 draft.js를 사용해서 만든 텍스트 창에 툴바를 넣어서 만든거기 때문이다.
  문제점 2: getImmutable이라고 수정할 수 없게끔 만들었기 때문이다.
  해결책 : getImmutable을 true로 해주면 된다. 그러면 어떻게 true로 바꿀 수 있을까?
  - <https://newdevzone.com/posts/how-to-displayed-local-content-react-draft-wysiwyg>
  - <https://stackoverflow.com/questions/36499858/draft-js-persist-editorcontent-to-database> : 자세히 읽어보기 -> 왜 항상 간단한 방법으로 끝이 날갛ㅎㅎㅎㅎㅎㅎㅎㅎㅎㅎㅎㅎㅎㅎㅎㅎㅎㅎㅎㅎ하하하하ㅏ하하하하하하하핳하하하ㅏ

### put image

- <https://so99ynoodles.com/ko/blog/make-wysiwyg-editor-with-draft-js>

## React Hook From

<https://codesandbox.io/s/5h1q5>

## 동적으로 글씨 크기 바꾸기

<https://developer-talk.tistory.com/131>

## 모바일 사이즈

- <https://codesandbox.io/s/k2x7l5jy27> : 버거 버튼?
- <https://www.framer.com/docs/examples/> : 버커 버튼 에니메이션 -> framer-motion(varient)

## Home 페이지 화면 디자인 구상

![download1](https://user-images.githubusercontent.com/96654391/185762515-d5ef009f-8a7b-4a9c-879e-5041c8e65655.png) <br>

![download2](https://user-images.githubusercontent.com/96654391/185762517-29391446-91bf-4d3a-a80b-945cd1a0d778.png)

## 서버 연결 tlqkf

- <https://qnrjs42.blog/react/react-cors>
- <https://doinge-coding.tistory.com/entry/Nginx-React-Springboot-%EC%97%B0%EB%8F%99>

### 프록시 서버 설정

1.  Chrome 메뉴 > 설정 > 고급 설정 표시 > 프록시 설정 변경… > LAN 설정으로 이동하여 '사용자 LAN에 프록시 서버 사용'을 선택 취소합니다.
    설정 -> 시스템 -> 프록시 설정
    프록시 default:
    자동으로 설정 검색: 켬
    설정 스크립트 사용: 끔
    프록시 서버 사용: 끔
2.  DNS Client
    검색 -> run -> 클릭 -> DNS Client -> 새로 고침

## 이미지 Layout

### Sigle

- <https://medium.com/workbench/floating-parallax-images-with-react-and-framer-motion-2f3703a8a070>

### Multi

- <https://blog.maximeheckel.com/posts/advanced-animation-patterns-with-framer-motion/> -<https://blog.logrocket.com/exploring-motion-one-framer-motion/>
