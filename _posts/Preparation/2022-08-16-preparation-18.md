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

```js
import React, { Component } from "react";
import { render } from "react-dom";
import { EditorState } from "draft-js";
import { Editor } from "react-draft-wysiwyg";
import { stateToHTML } from "draft-js-export-html";
import { stateFromHTML } from "draft-js-import-html";

function uploadImageCallBack(file) {
  return new Promise((resolve, reject) => {
    const xhr = new XMLHttpRequest();
    xhr.open("POST", "https://api.imgur.com/3/image");
    xhr.setRequestHeader("Authorization", "Client-ID XXXXX");
    const data = new FormData();
    data.append("image", file);
    xhr.send(data);
    xhr.addEventListener("load", () => {
      const response = JSON.parse(xhr.responseText);
      resolve(response);
    });
    xhr.addEventListener("error", () => {
      const error = JSON.parse(xhr.responseText);
      reject(error);
    });
  });
}

class EditorContainer extends Component {
  constructor(props) {
    super(props);
    this.state = {
      editorState: EditorState.createEmpty(),
    };
  }

  onEditorStateChange: Function = (editorState) => {
    // console.log(editorState)
    this.setState({
      editorState,
    });
  };
  exportHTML = () => {
    this.setState({
      convertedContent: stateToHTML(this.state.editorState.getCurrentContent()),
    });
  };

  updateHTML = (e) => {
    e.preventDefault();
    this.setState({ convertedContent: e.target.value });
  };

  importHTML = () => {
    const { editorState } = this.state;
    this.onChange(
      EditorState.push(editorState, stateFromHTML(this.state.convertedContent))
    );
  };

  render() {
    const { editorState } = this.state;
    return (
      <div className="EditorContainer">
        <div className="editor">
          <Editor
            editorState={editorState}
            onEditorStateChange={this.onEditorStateChange}
            placeholder="content"
            toolbar={{
              options: [
                "blockType",
                "fontSize",
                "inline",
                "list",
                "textAlign",
                "history",
                "image",
              ],
              list: { inDropdown: true },
              textAlign: { inDropdown: false },
              link: { inDropdown: true },
              history: { inDropdown: false },
              image: {
                uploadCallback: uploadImageCallBack,
                alt: { present: true, mandatory: true },
              },
            }}
            wrapperClassName="wrapper_class"
            editorClassName="editor_class"
            toolbarClassName="toolbar_class"
          />
        </div>
        <div>
          <button onClick={this.exportHTML}>Export HTML</button>
          <button onClick={this.importHTML}>Import HTML</button>
        </div>
        HTML:
        <textarea
          onChange={this.updateHTML}
          value={this.state.convertedContent}
        />
      </div>
    );
  }
}

export default EditorContainer;
```

근데 문제는 컴포넌트를 나눠서 하면서 동시에 EditDiary에서 html로 바뀐 str을 받고 싶은 것,, 그럴려면 어떻게 해야되나,,,,,,,

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
