---
title: "5.2주차"
excerpt: "5.2주차"
categories: [Sensor Programming]
tags: [Cpp Programming, Cpp]
toc: true
toc_sticky: true
---

## 환경 설정 정리

1. 007의 전원 연결 및 이더넷 연결
2. 제어판 > 네트워크 및 인터넷 > 네트워크 및 공유 센터(어댑터 설정 변경) > 이더넷 클릭 > 192.168.1.8 / 255.255.255.0 입력
3. VNC Viewer Open
4. PyCharm Open > File > New Project
5. File > New Project를 만들기
6. Previously configured interpreter > 인터프리터로 python3 선택
7. File > setting > Deployment > Mappings > Deploament path : /home/pi/Documents/embedded > OK
8. 하단 중앙쪽에 no default server 클릭 -> 192.168.1.7 서버 선택
9. Tools > Deployment > uploads => 여기서 바로 VNC에 올라오지 않는 것인지 기존 파일에서 새로운 파일을 업로드 해야 새로운 폴더에 새로운 파일이 올라가는지는 잘 모르겠음.

## LED 모듈 회로도

<img width="481" alt="download2" src="https://user-images.githubusercontent.com/96654391/195380349-4792264f-08da-42fb-b09e-d2358ca6a425.png"> <br>

<img width="343" alt="download1" src="https://user-images.githubusercontent.com/96654391/195380488-7b5a33d2-e16b-4bc8-87db-e407a7cd5270.png">

```py
import RPi.GPIO as GPIO
import time

PIN_LED = 12    # BCM 12번 핀에 해당
GPIO.setmode(GPIO.BCM)      # Board랑 bCM 2가지 포트가 있음
# setup : 지정하는 핀의 입출력 모드를 지정하는 함수, GPIO.OUT, GPIO.IN 중 하나를 입력
GPIO.setup(PIN_LED, GPIO.OUT)

def blink(Num):
    for i in range(1, Num):
        # output : 출력핀에 대한 상태를 지정해주는 함수
        # HIGH: 5v, LOW : 0v
        GPIO.output(PIN_LED, GPIO.HIGH)
        time.sleep(i)
        GPIO.output(PIN_LED, GPIO.LOW)
        time.sleep(1)

# input을 받는 것은 무조건 str로 들어온다.
In = int(input("Give times you want: "))
blink(In)
print("Program is terminated..!")
# cleanup : GPIO 모듈의 모든 리소스들을 해제, 연결된 핀들을 해제해준다는 것 같음
GPIO.cleanup()
```

## RPi.GPIO 모듈

- A module to control Raspberry Pi GPIO channels
- This package provides a class to control the GPIO on a Raspberry Pi. <br>

참고 자료: <https://m.blog.naver.com/PostView.naver?blogId=pk3152&logNo=221368513358&navType=by>

### GPIO.setup()

지정하는 핀의 입출력 모드를 지정하는 함수이다. 입력과 출력중에 한가지를 지정해주시면 된다.

```
입력핀 설정
GPIO.setup(pin번호, GPIO.IN)

출력핀 설정
GPIO.setup(pin번호, GPIO.OUT)

ex) (BCM모드에서) GPIO.setup(17,GPIO.OUT)
     GPIO 17번핀을 출력핀으로 설정
```

### GPIO.output()

출력핀에 대한 상태를 지정해주는 함수이다.

```
출력핀에 5V를 내보낼 때 설정
GPIO.output(pin번호,GPIO.HIGH)
GPIO.output(pin번호,True)

출력핀에 0V를 내보낼 때 설정
GPIO.output(pin번호,GPIO.LOW)
GPIO.output(pin번호,False)
```

### GPIO.input()

입력핀으로 설정한 핀에 입력되는 값을 읽는다. ( 디지털 값만 해당됨 )
아날로그값을 읽을려면 따로 DAC모듈이 필요한거 같다.

```
GPIO.input(pin번호)
```

### GPIO.cleanup()

GPIO 모듈의 모든 리소스들을 해제해준다. GPIO 모듈과 연결된 핀들을 해제해준다는 것 같다. GPIO 모듈을 사용한 마지막에 적어주면 좋다.

```
GPIO.cleanup()
```

## Pin numbering

- the BOARD numbering system – 하드웨어적 결선을 따름
- the BCM numbering - This is a lower level way of working - it refers to the channel numbers on the Broadcom SOC.
- To specify which you are using (mandatory):

  ```py
  GPIO.setmode(GPIO.BOARD)
  or
  GPIO.setmode(GPIO.BCM)
  ```

- 결선 넘버링 확인을 위해서

```
mode = GPIO.getmode() → 결과값: GPIO.BOARD, GPIO.BCM or None
```

## GPIO - LED

```py
import RPi.GPIO as GPIO
import time

PIN_LED = 3
GPIO.setmode(GPIO.BCM)
GPIO.setup(PIN_LED, GPIO.OUT)

try:
    while True:
        GPIO.output(PIN_LED, False)
        time.sleep(1)

        GPIO.output(PIN_LED, True)
        time.sleep(1)
except KeyboardInterrupt:
    print("Cleaning up")
    GPIO.cleanup()
```

해당 코드에서 PIN_LED 번호만 바꾸면서 출력해봄. <br>

- 1번: ?
- 2번: 12번 위에 있는 LED로 초록색 동그라미 모양이다.
- 3번: 2번과 같은 LED가 파란색으로 불이 나온다.
- 4번: 2번과 같은 LED가 초록 + 파란색으로 불이 나온다.
- 5번: water pump
- 6번: 펜
- 7번: ?
- 8번: ?
- 9번: ?
- 10번: ?
- 11번: ?
- 12번: 내가 봤던 LED 번호임
- 13번: 색깔이 칠해져 있는 모터, 5번보다는 좀더 세게 모터가 돈다.
- 20번: 소리 부저
  <br>

참고 자료: <https://m.blog.naver.com/PostView.naver?blogId=pk3152&logNo=221368477491&navType=by> 여기 잘 나와있다. 라즈베리파이 카테고리로 가보면 확인 가능.

<img width="378" alt="download1" src="https://user-images.githubusercontent.com/96654391/194020971-ad7ba1fd-afa5-4aee-a92e-56b0e76ee1b9.png">

<br>

- lOW -> HIGH : rising Edge
- HIGH -> LOW : falling Edge

## 펄스 폭 변조(Pulse width modulation: PWM)

- 출력 가능한 최대전압 (5V) 을 기준으로 일정한 비율 (duty) 동안 High 를 유지하고 나머지는 Low 를 출력하여 그림과 같은 사각파 출력을 생성(그 외 자세한 내용: 5주차 교안)

## 평가기준

- 🌟 실용성: 평소에 유용한 것 <br>

  ex. 스마트 팜: 날씨가 좋으면 비닐하우스를 열고, 날씨가 좋지 않으면 비닐하우스를 닫아. -> 습도 센서 같은 것을 사용해서 할 수 있다.

- 실현 가능성 <br>

  ex. 도로 주행: 초당 몇 프레임 이상, 카메라로 도로 인식하는 것을 해보겠다. 그런거는 의미가 있을 수 있다. 실용성에도. HW 퍼포먼스가 좋은게 아니라서 한정된 자원에서 얼마나 실시간 성을 보장할 수 있는지.를 하는것도 ㄱㅊ. 나름대로 의미가 있다. <br>

  더 나아가면 작은 자동차 위에 보드가 올라가서 라이닝 픽션 => 이 라인을 따라가는 것.

- 참신한 것

## 팀 빌딩

2조: 박소현, 노현진, 손수경 <br>

- <https://forums.raspberrypi.com/>
- <https://all3dp.com/1/best-raspberry-pi-projects/>
