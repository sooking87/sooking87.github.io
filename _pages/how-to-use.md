---
layout: single
title: "How to Use"
permalink: /howtouse/
author_profile: true
sidebar_main: true
---

## How to Use🚀

Category -> PREPARATION / STUDY / WEB / ALGORITHM / BACKJOON / PROGRAMMERS / OpsyDopsy

- PREPARATION : 프로젝트 준비하면서 찾아본 자료(categories: [프젝 제목] / tags: [분야, 언어]
- STUDY(WEB 제외 프로그래밍 언어 공부)
  - **_Do it Java_** (categories: [Do it Java] / tags: [Java])
  - **_Algorithm_** (categories: [Algorithm Study] / tags: [Algorithm Study, Java, Algorithm])
  - **_혼공머_** (categories: [Ai Study] / tags: [Ai Study, Python])
  - **_명품 자바_** (categories: [Java Programming] / tags: [Java Programming, Java])
- WEB(WEB관련 언어 공부)
  - **_생활 코딩_** (categories:[생활 코딩] / tags: [생활 코딩, WEB])
  - **_React_** (categories: [React] / tags: [React, WEB])
- ALGORITHM(알고리즘 관련 문제 풀이 업로드)
  - **_Java_** (categories: [Algorithm Java, Backjoon Java] / tags: [Algorithm Study, Java, Algorithm, Backjoon])
- Backjoon
  - **_Java_** (categories:[Backjoon Java] / tags: [Backjoon, Java])
  - **_JavaScript_** (categories: [Backjoon JavaScript] / tags: [Backjoon, JavaScript])
- Programmers
  - **_Java_** (categories:[Programmers Java] / tags: [Programmers, Java]) /
- OpsyDopsy: **_개같은 코딩_** (categories: [OpsyDopsy])

Tags -> OpsyDopsy / WEB / Backjoon / Programmers / 그 외의 언어들

<https://kr.piliapp.com/emoji/list/>
-> 이모티콘
<br>
<https://inpa.tistory.com/entry/MarkDown-%F0%9F%93%9A-Emoji-%EC%9D%B4%EB%AA%A8%ED%8B%B0%EC%BD%98-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0?category=896668> -> 마크다운에서 이모티콘 사용하기 <br>

<hr>

## VSCode 언어별 사용법

- Java : ctrl + shift + p -> create java project를 누르면 어디 폴더에 넣을 것인지를 선택한 후, 패키지 이름을 설정하면 됨. 그 후, 파일의 제목은 클래스 이름이 되고, 그 후는 이클립스랑 유사
- Java Script : <https://velog.io/@eundada064/%EB%B0%B1%EC%A4%80-JavaScript-VSCode-%ED%99%98%EA%B2%BD-%EC%84%B8%ED%8C%85>
- html/css : 우측 하단에 go live를 누르면 서버를 통해서 웹을 열 수 있고, ctrl + b를 누르면 비스코드에서 바로 개인 경로를 통해서 웹을 열 수 있다.
- 아마 대부분의 언어가 ctrl + alt + n을 누르면 다른 json파일 조작 없이도 실행이 가능한 것 같다.
- C언어 : launch.json파일과 tasks.json 파일을 해당 폴더에 저장해 준 후, ctrl + alt + n을 누르면 알아서 컴파일, 실행 다됨 -> 다시 해보니, launch.json과 tasks.json 파일 조작 없이도 그냥 ctrl + alt + n만 누르면 실행 됨
  <br>

나같은 경우는 MingGW가 다운받아져 있는 상황이라서 이 링크 참고
<https://webnautes.tistory.com/1158>

```c
//task.json
{
    "version": "2.0.0",
    "runner": "terminal",
    "type": "shell",
    "echoCommand": true,
    "presentation": {
        "reveal": "always"
    },
    "tasks": [ //C++ 컴파일
        {
            "label": "save and compile for C++",
            "command": "g++",
            "args": [ "${file}", "-o", "${fileDirname}/${fileBasenameNoExtension}" ],
            "group": "build",
            //컴파일시 에러를 편집기에 반영
            //참고: https://code.visualstudio.com/docs/editor/tasks#_defining-a-problem-matcher

            "problemMatcher": {
                "fileLocation": [
                    "relative",
                    "${workspaceRoot}"
                ],
                "pattern": {
                    // The regular expression.
                    //Example to match: helloWorld.c:5:3: warning: implicit declaration of function 'prinft'

                    "regexp": "^(.*):(\\d+):(\\d+):\\s+(warning error):\\s+(.*)$",
                    "file": 1,
                    "line": 2,
                    "column": 3,
                    "severity": 4,
                    "message": 5
                }
            }
        }, //C 컴파일
        {
            "label": "save and compile for C",
            "command": "gcc",
            "args": [ "${file}", "-o", "${fileDirname}/${fileBasenameNoExtension}" ],
            "group": "build",
            //컴파일시 에러를 편집기에 반영
            //참고: https://code.visualstudio.com/docs/editor/tasks#_defining-a-problem-matcher

            "problemMatcher": {
                "fileLocation": [
                    "relative",
                    "${workspaceRoot}"
                ],
                "pattern": {
                    // The regular expression.
                    //Example to match: helloWorld.c:5:3: warning: implicit declaration of function 'prinft'

                    "regexp": "^(.*):(\\d+):(\\d+):\\s+(warning error):\\s+(.*)$",
                    "file": 1,
                    "line": 2,
                    "column": 3,
                    "severity": 4,
                    "message": 5
                }
            }
        },
        // // 바이너리 실행(Windows)
        {
            "label": "execute",
            "command": "cmd",
            "group": "test",
            "args": [
                "/C", "${fileDirname}\\${fileBasenameNoExtension}"
            ]
        }
    ]
}
```
노트북에서 수정