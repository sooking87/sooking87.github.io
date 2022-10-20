---
title: "중간고사"
excerpt: "중간고사"
categories: [Sensor Programming]
tags: [Cpp Programming, Cpp]
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

## 인터럽트 사용법

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

### 신호등 만들기

- 빨간불 2초
- 노란불 1초
- 파란불 4초 <br>

노란불에서 파란불로 바뀌게되면 부저에서 소리가 2번나고, 노란불에서 빨간불로 바뀌게 되면 소리가 1번 난다.
