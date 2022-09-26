---
title: "4.1주차"
excerpt: "4.1주차"
categories: [Sensor Programming]
tags: [Cpp Programming, Cpp]
toc: true
toc_sticky: true
---

## VNC Viewer 사용하기

- 어떤 아이피를 할당 받았는지
- 라즈랑 노트북이랑 같은 와이파이로 묶여있어야 된다. <br>

[참고링크](https://www.instructables.com/How-to-Setup-Raspberry-Pi-Without-Monitor-and-Keyb/)

### step 1

1. 라즈베리 파이에 SD 카드 메모리를 넣어주기
2. write를 클릭하면 백업
3. SD 카드를 다시 뺐다가 껴서 해당 디렉토리에 SSH 파일을 만들기(확장자 없음)

### step 2

1. 이더넷 연결선으로 007이랑 내 노트북을 연결시킨다.
2. SD 카드를 007에 낀다.
3. 전원을 킨다.

### step 3

1. PuTTy를 깐다.
2. HostName에 raspberrypi.local을 친다.
3. SSH 클릭
4. open 클릭

### step 4

login as: pi <br>
pi@raspberrypi.local's password: raspberry <br>
pi@raspberrypi:~ $ **_sudo raspi-config_** <br>

<br>

sudo raspi-config 애는 앞으로 연결할 때 계속 필요

### step 5

1. choose 3 Interfacing Options 를 클릭
2. P3 VNC 클릭

### step 6

ifconfig를 통해서 포트 번호 알기 -> VNC에 입력!

## 다음에 또 키려고 한다면

1. PuTTy에서 `169.254.192.172 ` 해당 번호를 치고 open
2. interfacing Options 들어가 -> VNC 클릭
3. VNC에서 포트 번호 입력
