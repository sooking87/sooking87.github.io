---
title: "[생활 코딩] React 실행 화면 구축하기 "
excerpt: "왜 계속 VSCode 파일 하나 때문에 다운이 안될까,,,결국 리액트에서 제공하는 codesandbox 이용,,,,,😒"
categories: [생활 코딩]
tags: [생활 코딩, WEB]
toc: true
toc_sticky: true
---

## 실행 화면 구축하는 방법

react를 사용하기 위해서는 npm 통해서 다운이 가능한데, npm 같은 경우는 Node/js의 app store같은 느낌이라서 우선 Node.js 다운이 필요하다. 그 후 공식 권장 방법은 `npx` 를 통한 다운 방법인데, npx같은 경우는 일회용이로 공간 낭비를 하지 않고 매번 최신 버전을 사용할 수 있다는 장점이 있지만 굳이 매번 최신 버전이 필요하지 않으므로 `npm` 을 통해서 다운을 받았다.
<br>

#### 다운 받는 방법
1. cmd 창에 `npm install -g create-react-app` 을 다운
2. 그 후 cmd 창에 `create-react-app -V` 을 통해서 버전 확인 겸 다운 확인
3. 바탕 화면에 react-app(이름은 자유) 폴더를 만든 후 cmd에서 해당 폴더 경로로 이동
4. cmd 창에서 `create-react-app` 입력
<br>

나 같은 경우는 여기서 계속 에러가 떴고, 이 문제는 전부터 계속 어딘가에서 발생했던 에러였다.....(C\Users\gram\AppData....여튼 이 문제 때문에 VSCode 도 못쓰고 있는뎅🤔) 그래서 찾아보았던 해결책

1. cmd 창에 `npm install`, `npm start` 를 입력하고 `npm run start` 입력하(옆에 창이 뜬다고 했는데) 해결된다고 했는데 나는 안됨ㅎ하하하하하ㅏ핳ㅎ
2. cmd 창에 `npm install -g react-scripts` 입력 -> `npm run start` 입력 여전히 안됨^^^하하하하ㅏ하하핳 10R
<br>

뭐,,,일단 빨리 리액트에 대해서 배워야 하는 것이 우선이라서 일단은 `CodeSandBox` 사용하기로 함...쩝
