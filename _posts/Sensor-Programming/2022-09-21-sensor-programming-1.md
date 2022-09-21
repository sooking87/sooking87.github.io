---
title: "3.2주차"
excerpt: "3.2주차"
categories: [Sensor Programming]
tags: [Cpp Programming, Cpp]
toc: true
toc_sticky: true
---

## 명령어

- cd: 파일 경로 이동
  - cd .. :상위 디렉토리로 이동
  - cd /mnt/c/: 윈도우의 c 파일이 마운트된 경로. HD, 저장장치가 연결, OS에서 보이면 이걸 마운트라고 한다.
- clear: 화면 정리
- ls: 무슨 명령어든지 --h 또는 --help를 치게 되면 그 명령어를 어떻게 쓰는지 메뉴얼을 보여준다.
  - ls -a: all, 해당 디렉토리 밑에 있는 디렉토리들을 전부 다 보여달라.
  - ls -al or ls -l or ls -a, ls alh: 상세하게 보여준다. alh는 human readable. 여튼 ls는 그 디렉토리 안에 들어있는 디렉토리 보기
  - pwd: 현재 절대 경로
  - mkdir: 디렉토리 만들기
  - touch test.txt : txt 파일 만들기
  - rm: 파일을 지우는 명령어
  - re -r: 해당 디렉토리에 있는 파일을 반복적으로 지우고 디렉토리까지 지우게됨.
- apt-get update
- apt-get upgrade
- apt-get install
- apt-get remove

## 링크

- ln -s /usr/bin/mkdir ./test : mkdir을 test라는 이름으로 링크(바로가기)를 만듬
- rm을 통해서 지울 수 있음.

## 라즈베리파이 default Setting

1. use 메모리 같이 생긴게 sd 카드를 꽂고, 컴퓨터에 연결, 강의 교안에 rpi-imager 에 sd 카드 연결 => 이거 1주차 강의 교안에 있음
2. 빼서 라즈베리 파이에 넣고 전원 연결
3. 모니터에 hdmi 연결 마우스 키보드 연결, 큰 단자가 모니터로, 작은 단자가 라즈베리파이로 연결 || VNC Viewer 다운, 인터넷에 설치, 네트워크 연결 단자를 활용

## HW

SD 세팅 -> HDMI 연결을 통해서 라즈베리파이 UI가 나오는지를 확인
