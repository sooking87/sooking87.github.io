---
title: "6.2주차"
excerpt: "6.2주차"
categories: [Sensor Programming]
tags: [Sensor Programming, Python]
toc: true
toc_sticky: true
---

## 라즈베리 파이 구조 알기

<img width="431" alt="download1" src="https://user-images.githubusercontent.com/96654391/195379421-fd3c463e-ac2f-4b8f-b3a9-0384047de60f.png">

- I/O Adapter
- 라즈베리 파이
- 500M Pixel 카메라 모듈 <br>

  <https://syki66.github.io/blog/2020/10/31/picamera.html> <br>

  - `vcgencmd get_camera` : 카메라가 연결이 잘 되었는지 확인. supported, detected 둘다 1이 나와야 잘 연결이 된 것이다.
  - `raspistill -o picture1.jpg` : 사진 찍기

- 가스센서
- 인체감지
- 초음파 센서 -> 민
- 불꽃센서
- 조도센서
- 근접센서
- 온/습도센서 <br>
  라즈베리 4에서는 아직 적용이 안되어서 따로 모듈 추가가 필요하다고 한다. 하지만 나는 무서워서 일단 pass,,,, <br>

  관련 링크 1: <https://park-duck.tistory.com/entry/Python-%EB%9D%BC%EC%A6%88%EB%B2%A0%EB%A6%AC4-Adafruit-DHT1122%EC%98%A8%EC%8A%B5%EB%8F%84%EC%84%BC%EC%84%9C> <br>

  관련 링크 2: <https://blog.naver.com/PostView.nhn?blogId=emperonics&logNo=222092518468>

- 소리센서
- 워터펌트
- FAN
- 부저
- DC모터
- 서보모터
- LED 조명
- RGB 무드등

## GPIO - DC Motor

V = IR (E / (I | R)) 전압 전류 저항의 관계를 나타냄, V는 다른말로 E. 내가 E를 몰라 그거는 I \* R이라고. 내가 저항을 몰라 E / I라고, I를 몰라도 E / R이라는 거다. <br>

라즈베리파이에서의 GPIO 전압은 3.3V 또는 5V이다. 뭐가 되었든 specification을 통해서 led는 몇 볼트가 필요한지, 다 나와있다. 예를 들어서 led가 5A이라면 5/5 즉 1옴의 저항이 필요하다. 만약에 5mA라면 1mA = 0.001A이고 5 / 0.005이라면 저항은 1000옴짜리를 달아야된다. <br>
