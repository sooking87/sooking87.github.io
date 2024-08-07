---
title: "7.2주차"
excerpt: "7.2주차"
categories: [Sensor Programming]
tags: [Sensor Programming, Python]
toc: true
toc_sticky: true
---

## 시험 공지

시험은 월요일(24일) <br>

우리꺼는 가져와도 상관은 없어. 2시간 시험에, 이론도 보고 실습도 본다. <br>

먼저 이론 시험을 본다. 이걸 다 작성하면 이거 제출하고 문제지를 바꾸어 간다. <br>

그런 다음 실습문제를 풀면 된다. 시간 안배를 잘해라,,,,모두 다 통로쪽에 앉아라. <br>

시험지 펜으로만 가능. 연필은 감점. 이론 시험은 올려놓고 보지 말고 실습은 상관 없다. 검색도 상관없고 다 상관없다. 실습 시험은 오픈북. <br>

서술형. 파이썬 기초,,,,,,,,는 냄. 리눅스는 안냄. 이론 시험은 개념에 대해서 잘 숙지하고 있는 과정이기 때문에 수어동안에 배웠던 중요한 개념을 잘 이해하고 서술할 수 있는 정도. 잘 이해하고 있는지에 대한 문제를 낸다. <br>

중요한 몇몇 개념들을 잘 이해하고 있는지 문제에 나옴. 강사님 기준,,,,,,,,,,,1시간 50분 볼 수 있는 ,, 적절한 양으로,,,?

## Proximity Sensor(근접 센서)

물리적인 접촉 없이 전자계의 힘을 이용하여 물체의 존재 여부, 통과, 연속흐름, 적체 등의 감지 및 위치 제어에 이용하는 장치이다.

### 근접 센서의 종류

- 자기 근접센서: 가까워진 물체의 자기 유도 현상을 검출하는 방식. <br>

  자기 근접 센서는 자성체가 아니지만 전류를 흘려보내 자성이 생기게 된다. 즉, 주변으로 자기상이 생기게 된다. 근데 자기장이 방해를 받으면 그 파향이 바뀌게 되고 그걸 이용해서 방해물이 지나가 자기장의 왜곡이 있는지 없는지를 인지하는 원리이다.

- 홀센서 기반: 자기장을 이용
- 광학 근접 센서: 빛을 이용 <br>

  하나는 빛을 발사하고 하나는 감흥을 한다.

  ![다운로드](https://user-images.githubusercontent.com/96654391/196693824-b0c7505f-f2d3-48b2-ac58-5da9fa18d161.jpg) <br>

  파란색이 광학 근접 센서가 보내는 영역인데, 그 영역 안에 아무것도 없으면 센서가 정해놓은 특정 세기를 받는다. <br>

  만약에 방해물이 들어오게 되면 빛 반사를 통해서 빛이 세지게 되고 이를 통해서 근접한 것을 인지할 수 있다. 그림에서 발간색이 달라진 신호이고 이를 통해서 인지가 가능하다.

### Proximity_Sensor.py

```py
import RPi.GPIO as GPIO
import signal
import sys
import time

def signal_handler(signal, frame):
    print("pricess stop")
    GPIO.cleanup()
    sys.exit(0)

signal.signal(signal.SIGINT, signal_handler)

GPIO.setmode(GPIO.BCM)
# 근접 센서 핀 번호
COLLISION = 22
GPIO.setup(COLLISION, GPIO.IN)

while True:
    if GPIO.input(COLLISION) == 1:
        print("Carefull ~~ Ooooooops")
    if GPIO.input(COLLISION) == 0:
        print("Not Collision")
    time.sleep(0.2)
```

GPIO.input 값이 1이라는 근접했다는 뜻, 그렇지 않다면 0을 의미한다. 여기서 피피티 실습 코드랑은 0과 1의 위치가 반대로 되어있지만,, 이거는 연결 문제인 것 같기도 하다.

### 🌟 Proximity_Sensor2.py

앞차와 접근 시 경고음을 3회 발생합니다. 근접 센서를 사용하여 근접 시 beep음을 3회 발생하는 응용 프로그램을 작성해 보세요.

```py
import RPi.GPIO as GPIO
import time
import sys
import signal

GPIO.setmode(GPIO.BCM)
COLLISION = 22
Buzer = 20
GPIO.setup(COLLISION, GPIO.IN)
GPIO.setup(Buzer, GPIO.OUT)

while True:
    #
    if GPIO.input(COLLISION) == 1:
        print("Carefull ~~ Ooooooops")
        GPIO.output(Buzer, GPIO.HIGH)
    # 기본적으로 high 내가 쏜 및이 온다. 빛이 방해를 받으면 신호가 1이 아니게 된다.
    if GPIO.input(COLLISION) == 0:
        print("Not Collision")
        GPIO.output(Buzer, GPIO.LOW)

    time.sleep(0.2)
```

일반적으로 1이고, 막으면 0이 된다. 내꺼는 반대로 되어 있는듯? -> 바뀜... 이상하지만, ㅎ <br>

여기서 하나의 센서에 대해서 두 개의 이벤트를 처리할 수 없다고 말이 나왔던 이유: <br>

만약에 이벤트를 처리하기 위해서는

```py
import RPi.GPIO as GPIO
import time
import sys
import signal

def signal_handler(signal, frame):
    print("pricess stop")
    GPIO.cleanup()
    sys.exit(0)

# 충동시 이벤트 처리 함수
def carefull(channel):
    GPIO.output(SOUND, GPIO.HIGH)

# 근접하지 않았을 경우 이벤트 처리 함수
def carefull(channel):
    GPIO.output(SOUND, GPIO.LOW)

signal.signal(signal.SIGINT, signal_handler)

GPIO.setmode(GPIO.BCM)
COLLISION = 22
SOUND = 20
GPIO.setup(COLLISION, GPIO.IN)
GPIO.setup(SOUND, GPIO.OUT)

# 이벤트 처리
GPIO.add_event_detect(COLLISION, GPIO.RISING, callback=carefull)
GPIO.add_event_detect(COLLISION, GPIO.FALLING, callback=notColi)

while True:
    if GPIO.input(COLLISION) == 0:
        print("Carefull ~~ Ooooooops")


    if GPIO.input(COLLISION) == 1:
        print("Not Collision")

    time.sleep(0.2)
```

이렇게 코드를 작성할 수 있을 것이다. 하지만 이렇게 된다면 `RuntimeError: Conflicting edge detection already enabled for this GPIO channel` 이와 같은 에러가 나서 하나의 센서에 두개의 이벤트를 처리할 수 없다고 나오는 것 같다.

### Proximity_Sensor3.py

전압 변화를 확인하기 위해서 작성한 코드 <br>

#### 🌟 이벤트 처리 예시 코드

```py
import RPi.GPIO as GPIO
import sys
import time
import signal

GPIO.setwarnings(False)
def signal_handler(signal, frame):
    print("process stop")
    GPIO.cleanup()
    sys.exit(0)

signal.signal(signal.SIGINT, signal_handler)

# 카운터 값을 하나 증가해준다.
def my_callback(channel):
    global eventCounter
    eventCounter += 1
    global humandetect
    humandetect = 1

GPIO.setmode(GPIO.BCM)

## 근접 센서
### 1: Not Detect / 0: Proxy Detect
PROXY = 22
GPIO.setup(PROXY, GPIO.IN)

# global
eventCounter = 0
humandetect = 0
counter = 0

GPIO.add_event_detect(PROXY, GPIO.FALLING, callback=my_callback)

while True:
    if humandetect == 1:
        print("Detect %d" %eventCounter)
        humandetect = 0
        while not GPIO.input(PROXY):
            counter += 1
            print("Low %d " %counter)
            time.sleep(1)
        counter = 0
    else:
        print("No detect")
    time.sleep(0.5)
```

동작 원리는 default가 전압 5V이고, 어떤 물체가 근접한 경우는 0으로 떨어진다고 했다. 따라서 이벤트를 1에서 0으로 바뀐 FALLING인 경우 my_callback으로 넘어가도록 코드를 짰고, 그 안에 `while not GPIO.input(PROXY)` 를 통해서 0일 때(근접해있는 동안) 반복문을 계속 돌도록 했다.

```
No detect
No detect
No detect
No detect
Detect 2
Low 1
Low 2
Low 3
Low 4
Low 5
Low 6
Low 7
Detect 3
No detect
No detect
No detect

```

이렇게 출력이 되었다면 처음에는 1이므로 detect되지 않다가 근접했을 때, 반복문을 돌리면서 계속 Low를 출력하는 것을 확인할 수 있다 .

## Gas Sensor

가스 센서 원리정도만 알면 될 것 같다. 감흥하는 센서 표면에 이상물질이 표면에 닿으면 전기 현상이 일어난다. 공기 외의 신호가 들어온다면 뭔가 다른 가스가 있음을 감지한다.

### 🌟 이벤트

- GPIO.add_event_detect(GAS_IN, GPIO.FALLING, callback=my_callback, bouncetime=정수)

  - channel: GAS_IN 입력 채널 번호
  - 신호 발생 이벤트: Falling/Rising 타입
  - 해당 이벤트 발생 시 실행할 사용자 callback 함수 지정
  - Bouncetime=정수

- GPIO.remove_event_detect(channel) <br>

  이벤트도 제거가 필요하다. 이벤트 핸들러가 많을수록 느려지므로 불필요한 이벤트 인터럽트는 제거가 필요하다.

## 불꽃 감지 센서

불꽃에서 방출되는 특정 파장 대역의 에너지를 흡수 및 검출하여 불꽃의 존재 유무, 위치를 센싱한다.

## 시험 예상 문제

### 가까워지면 서보 모터를 90도 돌리는 문제

```py
import RPi.GPIO as GPIO
import time

GPIO.setmode(GPIO.BCM)
GPIO_TRIGGER = 18
GPIO_ECHO = 21
GPIO_MOTOR = 23

GPIO.setup(GPIO_TRIGGER, GPIO.OUT)
GPIO.setup(GPIO_ECHO, GPIO.IN)
GPIO.setup(GPIO_MOTOR, GPIO.OUT)

PWM_RC=GPIO.PWM(GPIO_MOTOR, 100)
PWM_RC.start(7.5)

try:
    while True:
        stop = 0
        start = 0
        # 먼저 트리거 핀을 OFF 상태로 유지한다.
        GPIO.output(GPIO_TRIGGER, False)
        time.sleep(2)

        GPIO.output(GPIO_TRIGGER, True)
        time.sleep(0.00001)
        GPIO.output(GPIO_TRIGGER, False)

        # 에코핀이 ON되는 시점을 시작 시간으로 잡는다.
        while GPIO.input(GPIO_ECHO) == 0:
            start = time.time()

        # 에코 핀이 다시 OFF되는 시점을 반사파 수신 시간으로 잡는다.
        while GPIO.input(GPIO_ECHO) == 1:
            stop = time.time()

        # Calculate pulse length
        elapsed = stop - start

        if (stop and start):
            distance = (elapsed * 34000.0) / 2
            if distance <= 10:
                PWM_RC.ChangeDutyCycle(5)
                time.sleep(1)
                PWM_RC.ChangeDutyCycle(95)
                time.sleep(1)

except KeyboardInterrupt:
    print("Ultrasoic Distance Measurement End")
    GPIO.cleanup()

# Reset GPIO settings
GPIO.cleanup()
```
