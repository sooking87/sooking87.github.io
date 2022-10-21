---
title: "4.1주차"
excerpt: "4.1주차"
categories: [Sensor Programming]
tags: [Sensor Programming, Python]
toc: true
toc_sticky: true
---

## VNC Viewer 사용하기

- 어떤 아이피를 할당 받았는지
- 라즈랑 노트북이랑 같은 와이파이로 묶여있어야 된다. <br>

[참고링크](https://www.instructables.com/How-to-Setup-Raspberry-Pi-Without-Monitor-and-Keyb/)

## 다시 정리

SD카드 다시 Write(환경 설정에서 raspberrypi.local 체크, 사용자 설정: pi / raspberry 로 체크) -> 쓰기가 완료되면 SD카드 뺐다가 다시 끼기 -> SD카드에 SSH (확장자 없음) 파일 추가 -> putty 다운로드(있다면 삭제했다가 다시 다운로드) -> raspberrypi.local, ssh선택 -> sudo raspi-config -> 3. interface -> VNC선택 -> VNC Viewer에서 raspberrypi.local 검색 -> 라즈베리파이 터미널 열기 -> `sudo nano /etc/dhcpcd.conf` 입력 ->

```
interface eth0
static ip_address=192.168.1.7/24
static router=192.168.1.1
```

입력 -> Ctrl + O를 통해서 저장 Ctrl + X를 통해서 눌러 닫기 -> 라즈베리파이 전원 뺐다가 다시 끼기 -> 노트북이랑 이더넷 연결 -> 제어판 > 네트워크 및 인터넷 > 네트워크 및 공유 센터(어댑터 설정 변경) > 이더넷 클릭 > 192.168.1.8 / 255.255.255.0 입력 -> VNC Viewer에 192.168.1.7 검색 들어가,,,,,,,,tlqkf,,,,
