---
title: "중간고사"
excerpt: "중간고사"
categories: [Sensor Programming]
tags: [Sensor Programming, Python]
toc: true
toc_sticky: true
---

## GPIO 주요 핀 번호

- 12번 : LED
- 13번 : DC 모터
- 20번 : 부저
- 2번 : R LED
- 3번 : G LED
- 4번 : B LED
- 19번 : RGB Power
- 5번 : Water Pump
- 6번 : Fan
- 23번 : 서보 모터
- 27번 : 모션 센서(PLR_Sensor)
- 18번 : GPIO_TRIGGER
- 21번 : GPIO_ECHO
- 22번 : 근접 센서

## GPIO 모듈

<https://sooking87.github.io/sensor%20programming/sensor-programming-4/>

## 🌟 인터럽트 처리

시그널을 통해서 처리하고, 여기서 시그널 핸들러 함수의 경우는 시그널이 발생했을 때, 발생해야되는 코드를 함수 부분에 넣어주면 된다.

```py
def signal_handler(signal, frame):
    print('process stop')
    GPIO.cleanup()
    sys.exit(0)

# Signal 수신 함수. signal(시그널:interrupt, 이벤트 핸들러 함수)
signal.signal(signal.SIGINT, signal_handler)
```

이렇게만 처리해주면 알아서 처리하는 듯?

## 🌟 이벤트 처리

- GPIO.add_event_detect(channel, GPIO.FALLING/RISING, callback=my_callback, bouncetime=정수)

  - 채널 부분에는 해당 핀 번호를 입력하면 된다.
  - bouncetime: 스위치를 눌렀을 때 발생할 수 잇는 바운싱 또는 채터링을 막기 위해 delay 시간을 주는 것(ms)

- GPIO.remove_event_detect(channel)

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

### 약, 중, 강 입력값에 따라 펜 돌리기

약(R), 중(G), 강(B) 입력값에 따라 펜 돌리기 + RGB LED까지 출력

```py
import RPi.GPIO as GPIO
import sys
import time
import signal

GPIO.setwarnings(False)


def signal_handler(signal, frame):
    print('process stop')
    GPIO.cleanup()
    sys.exit(0)

# Signal 수신 함수. signal(시그널:interrupt, 이벤트 핸들러 함수)
signal.signal(signal.SIGINT, signal_handler)


# defualt
# Pin num
FAN = 6
RGBPOWER = 19
RED = 4
GREEN = 3
BLUE = 2
# set
GPIO.setmode(GPIO.BCM)
GPIO.setup(FAN, GPIO.OUT)

GPIO.setup(RGBPOWER, GPIO.OUT)
GPIO.setup(RED, GPIO.OUT)
GPIO.setup(GREEN, GPIO.OUT)
GPIO.setup(BLUE, GPIO.OUT)
# PWM 인스턴스 만들기
PWM_FAN = GPIO.PWM(FAN, 100)
PWM_FAN.start(0)

GPIO.output(RGBPOWER, 1)
# start
while True:
    command = input("low / middle / high / off: ")
    if (command == "low"):
        # time.sleep(1) # turnOn 1초 뒤에 turnOnFan 시작
        PWM_FAN.ChangeDutyCycle(30)
        GPIO.output(RED, 1)
        # GPIO.output(BLUE, 0)
        # GPIO.output(GREEN, 0)
        # GPIO.add_event_detect(RED, GPIO.RISING, callback=blink)

    elif (command == "middle"):
        PWM_FAN.ChangeDutyCycle(60)
        GPIO.output(RED, 0)
        GPIO.output(BLUE, 0)
        GPIO.output(GREEN, 1)

    elif (command == "high"):
        PWM_FAN.ChangeDutyCycle(100)
        GPIO.output(RED, 0)
        GPIO.output(BLUE, 1)
        GPIO.output(GREEN, 0)

    else:
        PWM_FAN.ChangeDutyCycle(0)
        GPIO.output(RGBPOWER, 0)
        GPIO.output(RED, 0)
        GPIO.output(BLUE, 0)
        GPIO.output(GREEN, 0)
        GPIO.cleanup()
        sys.exit(0)
```

### 신호등 만들기

- 빨간불 2초
- 노란불 1초
- 파란불 4초 <br>

노란불에서 파란불로 바뀌게되면 부저에서 소리가 2번나고, 노란불에서 빨간불로 바뀌게 되면 소리가 1번 난다.

```py
import RPi.GPIO as GPIO
import sys
import time
import signal

GPIO.setwarnings(False)

def signal_handler(signal, frame):
    print('process stop')
    GPIO.cleanup()
    sys.exit(0)

# Signal 수신 함수. signal(시그널:interrupt, 이벤트 핸들러 함수)
signal.signal(signal.SIGINT, signal_handler)

def setRGB(r, g, b):

    PWM_RED.ChangeDutyCycle(r)
    PWM_GREEN.ChangeDutyCycle(g)
    PWM_BLUE.ChangeDutyCycle(b)

def Buzz(t):
    for i in range(t):
        GPIO.output(BUZ, 1)
        time.sleep(0.3)

        GPIO.output(BUZ, 0)
        time.sleep(0.3)
        # GPIO.output(LED, 1)
        # time.sleep(1)
        #
        # GPIO.output(LED, 0)
        # time.sleep(1)


# default
# pin num
BUZ = 20
RGBPOWER = 19
RED = 4
GREEN = 3
BLUE = 2

## 부저가 너무 시끄러워서 일단 LED로 대체ㅐ
LED = 12
# set
GPIO.setmode(GPIO.BCM)
GPIO.setup(BUZ, GPIO.OUT)
GPIO.setup(RGBPOWER, GPIO.OUT)
GPIO.setup(RED, GPIO.OUT)
GPIO.setup(GREEN, GPIO.OUT)
GPIO.setup(BLUE, GPIO.OUT)
GPIO.setup(LED, GPIO.OUT)

# PWM
PWM_RED = GPIO.PWM(RED, 100)
PWM_RED.start(100)
PWM_GREEN = GPIO.PWM(GREEN, 100)
PWM_GREEN.start(0)
PWM_BLUE = GPIO.PWM(BLUE, 100)
PWM_BLUE.start(0)


GPIO.output(RGBPOWER, True) # 이거 꼭!
while True:

    # 빨간불 2초
    setRGB(1, 0, 0)
    time.sleep(2)
    # 노란불 1초
    setRGB(1, 1, 0)
    time.sleep(1)
    Buzz(2)

    # 파란불 4초
    setRGB(0, 0, 1)
    time.sleep(4)
    # 노란불 1초
    setRGB(1, 1, 0)
    time.sleep(1)
    Buzz(1)
```

### 모션 센서에 모션이 감지되면 빨간불 3번과 소리 3번이 교차로 발생

```py

```

### 자동차 후방 감지기

- 5cm 이내 접근: led 빨간색 + 부저(0.2s)
- 10cm 이내 접근: led 노란색 + 부저(0.5s)
- 20cm 이내 접근: led 초록색 + 부저(1s)
- 그외 파란색

```py
import RPi.GPIO as GPIO
import time
import sys
import signal

GPIO.setwarnings(False)

def signal_handler(signal, frame):
    print('process stop')
    GPIO.cleanup()
    sys.exit(0)

# Signal 수신 함수. signal(시그널:interrupt, 이벤트 핸들러 함수)
signal.signal(signal.SIGINT, signal_handler)

def setRGB(r, g, b):
    PWM_RED.ChangeDutyCycle(r)
    PWM_GREEN.ChangeDutyCycle(g)
    PWM_BLUE.ChangeDutyCycle(b)


# default
# PIN NUM
TRIGGER = 18
ECHO = 21
RGBPOWER = 19
R = 4
G = 3
B = 2
BUZ = 20

# SET
GPIO.setmode(GPIO.BCM)
GPIO.setup(TRIGGER, GPIO.OUT)
GPIO.setup(ECHO, GPIO.IN)
GPIO.setup(RGBPOWER, GPIO.OUT)
GPIO.setup(R, GPIO.OUT)
GPIO.setup(G, GPIO.OUT)
GPIO.setup(B, GPIO.OUT)
GPIO.setup(BUZ, GPIO.OUT)

# PWM(PIN, Hz)
PWM_BUZ = GPIO.PWM(BUZ, 1000)
PWM_BUZ.start(0)
PWM_RED = GPIO.PWM(R, 100)
PWM_RED.start(0)
PWM_GREEN = GPIO.PWM(G, 100)
PWM_GREEN.start(0)
PWM_BLUE = GPIO.PWM(B, 100)
PWM_BLUE.start(0)

GPIO.output(RGBPOWER, 1)
while True:
    stop = 0
    start = 0

    GPIO.output(TRIGGER, False)
    time.sleep(0.5)

    GPIO.output(TRIGGER, True)
    time.sleep(0.00001)
    GPIO.output(TRIGGER, False)

    while GPIO.input(ECHO) == 0:
        start = time.time()

    while GPIO.input(ECHO) == 1:
        stop = time.time()

    elapsed = stop - start

    if (stop and start):
        distance = (elapsed * 34000) / 2
        print("Distance: %.1f cm" %distance)

        # 가까이 올수록 소리가 높아지는 경우
        if (distance <= 20):
            REDPercent = abs(100 - distance)
            GREENPercent = abs(50 - distance)
            BLUEPercent = abs(10 - distance)

            PWM_BUZ.ChangeFrequency(1000)

            for i in range(5):
                setRGB(REDPercent, GREENPercent, BLUEPercent)
                PWM_BUZ.ChangeDutyCycle(20)
                time.sleep(0.01 * distance)

                PWM_BUZ.ChangeDutyCycle(0)
                time.sleep(0.01 * distance)
        else:
            setRGB(0, 0, 100)
```
