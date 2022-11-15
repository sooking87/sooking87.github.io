---
title: "9.1주차 9.2주차 10.1주차 10.2주차"
excerpt: "9.1주차 9.2주차 10.1주차 10.2주차"
categories: [Sensor Programming]
tags: [Sensor Programming, Python]
toc: true
toc_sticky: true
---

## 9.1주차, 9.2주차

-> 프로젝트 발표 수업

## 10.1주차

### VNC 적용 찐찐막

SD카드 다시 Write(환경 설정에서 raspberrypi.local 체크, 사용자 설정: pi / raspberry 로 체크) <br>
-> 쓰기가 완료되면 SD카드 뺐다가 다시 끼기 <br>
-> SD카드에 SSH (확장자 없음) 파일 추가 <br>
-> putty 다운로드(있다면 삭제했다가 다시 다운로드) <br>
-> raspberrypi.local, ssh선택 <br>
-> sudo raspi-config <br>
-> 3. interface -> VNC선택 <br>
-> VNC Viewer에서 raspberrypi.local 검색 <br>
-> 라즈베리파이 터미널 열기 <br>
-> `sudo nano /etc/dhcpcd.conf` 입력 ->

```
interface eth0
static ip_address=192.168.1.7/24
static router=192.168.1.1 (오타 아님)
```

입력 <br>
-> Ctrl + O를 통해서 저장 Ctrl + X를 통해서 눌러 닫기 <br>
-> 라즈베리파이 전원 뺐다가 다시 끼기 <br>
-> 노트북이랑 이더넷 연결 <br>
-> 제어판 > 네트워크 및 인터넷 > 네트워크 및 공유 센터(어댑터 설정 변경) > 이더넷 클릭 > 192.168.1.8 / 255.255.255.0 입력 <br>
-> VNC Viewer에 192.168.1.7 검색 들어가,,,,,,,,tlqkf,,,, <br>

일단 여기까지 기본 설정 그런 다음 설정 방법 <br>

Preferences – Raspberry Pi Configuration 실행(Interfaces 메뉴에서 SSH, VNC, SPI, I2C 를 활성화 한 후 리부팅) <br>
-> 가상환경 설치

```py
~$ sudo apt install virtualenv
~$ virtualenv emb
~$ ls ./emb/
~$ source ./emb/bin/activate
(emb) pi@raspberrypi ~$:
```

-> wiringPi 설치

```py
(emb) wget https://project-downloads.drogon.net/wiringpi-latest.deb
(emb) sudo dpkg -i wiringpi-latest.deb
(emb) gpio -v
(emb) gpio readall
```

-> GPIO 모듈 다운

```py
(emb) pip install RPi.GPIO
# 설치 확인
(emb) python -c "import RPi.GPIO as GPIO; print(GPIO.VERSION)"
```

-> 파이참 연결,,, <br>
-> 카메라 설정 해야됨 <br>

```py
$ sudo nano /boot/config.txt
```

다음 옵션을 찾아 주석(#)을 해제한 후 값을 입력

```py
hdmi_force_hotplug=1
hdmi_group=1
hdmi_mode=16
hdmi_drive=2
```

## 10.2 주차

7 세그먼트 사용
