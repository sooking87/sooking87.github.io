---
title: "7.1주차"
excerpt: "7.1주차"
categories: [Sensor Programming]
tags: [Cpp Programming, Cpp]
toc: true
toc_sticky: true
---

# 007 Total 코드 리뷰

해당 학습 주차는 4, 5, 6, 7.1주차이다.

## led_blink.py

```py
import RPi.GPIO as GPIO
import time

# GPIO 12번에 해당하는 LED를 킨다.
PIN_LED = 12
# setmode -> BOARD, BCM
GPIO.setmode(GPIO.BCM)
# LED가 연결된 핀을 출력으로 설정
GPIO.setup(PIN_LED, GPIO.OUT)

try:
    while True:
        # LOW(0, 0V) 신호를 전송
        GPIO.output(PIN_LED, False)
        time.sleep(1)

        # HIGH(1, 5V) 신호를 전송
        GPIO.output(PIN_LED, True)
        time.sleep(1)
except KeyboardInterrupt:
    print("Cleaning up")
    GPIO.cleanup()
```

### GPIO.setup()

지정하는 핀의 **_입출력 모드를 지정_** 하는 함수이다. 입력과 출력중에 한가지를 지정해주시면 된다.

```
입력핀 설정
GPIO.setup(pin번호, GPIO.IN)

출력핀 설정
GPIO.setup(pin번호, GPIO.OUT)

ex) (BCM모드에서) GPIO.setup(17,GPIO.OUT)
     GPIO 17번핀을 출력핀으로 설정
```

### GPIO.output()

**_출력핀에 대한 상태_** 를 지정해주는 함수이다.

```
출력핀에 5V를 내보낼 때 설정
GPIO.output(pin번호, GPIO.HIGH)
GPIO.output(pin번호, True)

출력핀에 0V를 내보낼 때 설정
GPIO.output(pin번호, GPIO.LOW)
GPIO.output(pin번호, False)
```

### GPIO.cleanup()

GPIO 모듈의 모든 리소스들을 해제해준다. GPIO 모듈과 연결된 핀들을 해제해준다는 것 같다. GPIO 모듈을 사용한 마지막에 적어주면 좋다.

```
GPIO.cleanup()
```

## led_blink_2.py

```py
import RPi.GPIO as GPIO
import time

# BCM 12번 핀에 해당
PIN_LED = 12
# Board랑 bCM 2가지 포트가 있음
GPIO.setmode(GPIO.BCM)
# LED가 연결된 핀을 출력으로 설정
GPIO.setup(PIN_LED, GPIO.OUT)

def blink(Num):
    for i in range(1, Num):
        # High(1, 5V) 신호를 전송
        GPIO.output(PIN_LED, GPIO.HIGH)
        time.sleep(i)

        # LOW(0, 0V) 신호를 전송
        GPIO.output(PIN_LED, GPIO.LOW)
        time.sleep(1)

# input을 받는 것은 무조건 str로 들어온다.
In = int(input("Give times you want: "))
blink(In)
print("Program is terminated..!")
GPIO.cleanup()
```

1부터 입력받은 숫자까지 1초씩 늘려가면서 출력을 해주고, 중간중간 1초씩 LED를 끈다.

## led_pwm_hard.py

PWM은 디지털 소스를 사용하여 아날로그 신호를 생성하는 방법이다. 즉 이산적인 신호를 연속적으로 바꾸는 방법이다. <br>

![Depth-First-Search](https://user-images.githubusercontent.com/96654391/196194674-81582e5a-c98a-4f69-ac1f-43e5a8a66e7f.gif)

<br>

출력 가능한 최대 전압(5V)을 기준으로 일정한 비율(duty) 동안 High를 유지하고 나머지는 Low를 출력하여 그림과 같은 시각파 출력을 생성한다. <br>

PWM는 frequency와 duty cycle이라는 요소로 구성되어 있다.

- frequency: PWM이 사이클을 완료하는 속도 <br>

    <img width="600" alt="download1" src="https://user-images.githubusercontent.com/96654391/196182111-eec0ff32-9f01-4b07-83ed-dffc268f53e2.png">

- duty cycle: High 신호인 시간을 1, 사이클 완료에 걸리는 시간으로 나눈 백분율, 5V가 차지하는 정도, 즉, Duty Cycle = Pulse Width / Period \* 100 <br>
  <br>

High를 유지하는 비율(duty cycle)을 조절하여 정전압 아날로그 신호를 출력하는 것과 같은 효과를 낸다. <br>

- Hardward-PWM: 타이머 카운터와 인터럽트 사용
- Software-PWM: 딜레이를 사용, 다소 부정확, CPU에 과부하

```py
import RPi.GPIO as GPIO
from time import sleep

# BCM 12번 핀에 해당
PIN_LED = 12
# BCM 모드
GPIO.setmode(GPIO.BCM)
# 12번에 출력을 설정
GPIO.setup(PIN_LED, GPIO.OUT)

# PWM 주파수를 설정(1000Hz)
pi_pwm = GPIO.PWM(PIN_LED, 1000)
# 첫 duty cycle은 0(출력 X)
pi_pwm.start(0)

try:
    while True:
        for duty in range(0, 101, 1):
            # Duty Cycle을 0~100까지 비율을 증가
            pi_pwm.ChangeDutyCycle(duty)
            # 🌟이거 안넣으면 안됨
            sleep(0.01)
        # 🌟이거 안넣으면 안됨
        sleep(0.5)
        for duty in range(100, -1, -1):
            # Duty Cycle을 100~0까지 비율을 감소
            pi_pwm.ChangeDutyCycle(duty)
            sleep(0.01)
        sleep(0.5)

except KeyboardInterrupt:
    print("Cleaning up")
    GPIO.cleanup()
```

## GPIO - DC Motor

- DC Motor는 **_공급 전류에 비례하여 회전 속도 및 회전력이 증가_** 함.
- DC Motor가 구현되면 내부 저항이 고정되므로 공급 전압에 따라 전류가 비례함
- 따라서 공급 전압에 따라 회전력, 회전 속도가 변함
- LED 밝기 제어 예제와 같은 콛르르 사용하여 일정한 짧은 시간 간격으로 ON 구간과 OFF 구간의 비율을 달리하여 DC Motor에 공급되는 전압을 가변하는 것과 동일한 효과 발생 -> 회전 속도 제어 가능. <br>

### 동작 원리

자기장 속의 도체에 전류가 흐를 때 발생하는 힘을 사용 :: 플레밍의 왼손 법칙 <br>

Permanent magnet을 사용하여 자계(자기장) 형성성한 후 도체에 전류를 흘려 회전력을 얻는다. 🌟 다시다시다시다시다시닷

### motor.py

```py
import RPi.GPIO as GPIO
import time

# BCM 13번 핀 사용
GPIO_RP = 13
# BCM 모드 사용
GPIO.setmode(GPIO.BCM)
# 13번 핀을 출력으로 설정
GPIO.setup(GPIO_RP, GPIO.OUT)

try:
    while True:
        print('forward')
        # True(5V) 신호를 보냄
        GPIO.output(GPIO_RP, True)
        time.sleep(1)

        print('stop')
        # False(0V) 신호를 보냄
        GPIO.output(GPIO_RP, False)
        time.sleep(5)

except KeyboardInterrupt:
    print("Motor activation is terminated....!!!")
finally:
    GPIO.cleanup()
```

### motor2.py

```py
import RPi.GPIO as GPIO
import time

# PWM pin num 13
pin = 13

GPIO.setmode(GPIO.BCM)
GPIO.setup(pin, GPIO.OUT)
# frequuency = 50Hz
p = GPIO.PWM(pin, 50)

p.start(0)
cnt = 0

try:
    while True:
        # 5V * 0.01 = 0.05v를 주고 1초동안 기다림
        # ChangeDutyCycle(1)이므로 1%만큼 전력을 사용
        p.ChangeDutyCycle(1)
        print("angle: 1")
        time.sleep(1)

        # 5 * 0.05 = 0.25v를 주고 1초동안 기다림
        p.ChangeDutyCycle(5)
        print("angle: 5")
        time.sleep(1)

        # 5 * 0.08 = 0.4v를 주고 1초동안 기다림
        # v가 낮아도 상당히 잘 돈다. 왜 ? 기존 토큰이 좋아서.
        p.ChangeDutyCycle(8)
        print("angle: 8")
        time.sleep(1)
except KeyboardInterrupt:
    p.stop()
GPIO.cleanup()
```

### motor3.py

```py
import RPi.GPIO as GPIO
import time

pin = 13
GPIO.setmode(GPIO.BCM)
GPIO.setup(pin, GPIO.OUT)
p = GPIO.PWM(pin, 100)
p.start(0)
cnt = 0

try:
    while True:
        # 5V * 0.1 = 0.5V 주고 3초동안 기다림
        p.ChangeDutyCycle(10)
        print("Angle: 10")
        time.sleep(3)

        # 3초간 일시정지
        print("stop")
        GPIO.output(pin, False)
        time.sleep(3)

        # 5V * 0.35 = 1.75V 주고 3초동안 기다림
        p.ChangeDutyCycle(35)
        print("Angle: 35")
        time.sleep(3)

        # 3초간 일시정지
        print("stop")
        p.ChangeDutyCycle(pin, False)
        time.sleep(3)

        # 5V * 0.8 = 4V를 주고 3초동안 기다림
        p.ChangeDutyCycle(80)
        print("Angle: 80")
        time.sleep(3)

        # 3초간 일시정지
        print("stop")
        GPIO.output(pin, False)
        time.sleep(3)
except KeyboardInterrupt:
    p.stop()

GPIO.cleanup()
```

## Piezo 센서 제어

### 동작 원리

압전 효과

- 고체에 힘을 가하였을 때, 결정 겉면에 전기적 분극이 일어나는 현상을 피에조 저항 효과라고도 한다.
- 수정이나 로셀염 등의 결정에 압력을 가하면 전압이 발생하는데 이것을 압전 직접효과라고 한다.
- 금속판 사이에 얇은 압전 소자를 끼워 넣은 센서로 소리, 진동, 압력 등을 감지한다.

### piezo.py

#### 🌟 인터럽트 개념 🌟

interrupt, event driven(사건 지향)
event라는 것이 뭘까? 인터럽트란 간단히 말하면 기존의 CPU에서 처리하면 프로그램을 중단하고 인터럽트를 요청한 프로그램으로 실행 제어권을 넘기는 것을 말한다. <br>

인터럽트를 맡게 해주는 event handler가 event 발생을 감시 중,,

```py
import RPi.GPIO as GPIO
import signal
import sys
import time

# 각각의 signal에 대한 핸들러
def signal_handler(signal, frame):
    print('process stop')
    GPIO.cleanup()
    sys.exit(0)

# Signal 수신 함수. signal(시그널:interrupt, 이벤트 핸들러 함수)
signal.signal(signal.SIGINT, signal_handler)

# GPIO 20 (Wpi : 28)
BUZCONTROL = 20
# BCM Mode
GPIO.setmode(GPIO.BCM)
# 20번 핀을 출력으로 결정
GPIO.setup(BUZCONTROL, GPIO.OUT)

while True:
    print("here")
    GPIO.output(BUZCONTROL, 1)
    time.sleep(1)

    GPIO.output(BUZCONTROL, 0)
    time.sleep(1)
```

### piezo2.py

```py
import RPi.GPIO as GPIO
import time

GPIO.setwarnings(False)
# default
gpio_pin = 20
GPIO.setmode(GPIO.BCM)
GPIO.setup(gpio_pin, GPIO.OUT)

scale = [261, 294, 329, 349, 392, 440, 493, 523]
# gpio_pin의 주파수 100Hz인 PWM 인스턴스 생성
p = GPIO.PWM(gpio_pin, 100)
GPIO.output(gpio_pin, True)
# Duty Cycle 100%로 시작
p.start(100)
# Duty Cycle을 90%로 변경
p.ChangeDutyCycle(90)

while True:
    # 주파수를 scale의 음계를 변경
    p.ChangeFrequency(scale[4])
    time.sleep(0.5)
    p.ChangeFrequency(scale[4])
    time.sleep(0.5)
    p.ChangeFrequency(scale[5])
    time.sleep(0.5)
    p.ChangeFrequency(scale[5])
    time.sleep(0.5)
    p.ChangeFrequency(scale[4])
    time.sleep(0.5)
    p.ChangeFrequency(scale[4])
    time.sleep(0.5)
    p.ChangeFrequency(scale[2])
    time.sleep(0.5)

p.stop()
GPIO.cleanup()
```

## RGB Led제어

### RGB_led.py

```py
import RPi.GPIO as GPIO
import signal
import sys
import time

def signal_handler(signal, frame):
    print("process stop")
    GPIO.cleanup()
    sys.exit(0)

# 이벤트(또는 인터럽트)가 생겼을 때 시그널을 듣는애
signal.signal(signal.SIGINT, signal_handler)

# LED에 전원을 공급하는 핀
RGBLEDPOWER = 12
GPIO.setmode(GPIO.BCM)

RED = 2
GREEN = 3
BLUE = 4

GPIO.setup(RGBLEDPOWER, GPIO.OUT)
GPIO.setup(RED, GPIO.OUT)
GPIO.setup(GREEN, GPIO.OUT)
GPIO.setup(BLUE, GPIO.OUT)

for i in range(0, 10):
    GPIO.output(RGBLEDPOWER, 1)

    GPIO.output(RED, 1)
    GPIO.output(BLUE, 1)
    GPIO.output(GREEN, 0)
    time.sleep(1)

    GPIO.output(RED, 0)
    GPIO.output(BLUE, 1)
    GPIO.output(GREEN, 1)
    time.sleep(1)

    GPIO.output(RED, 1)
    GPIO.output(BLUE, 0)
    GPIO.output(GREEN, 1)
    time.sleep(1)
GPIO.output(GREEN, 0)

# RGB의 신호값을 바꾸면 색깔이 바뀐다.
```

R: 0, 1 <br>
G: 0, 1 <br>
B: 0, 1 <br>

여기서는 0, 1만 줄 수 있다. 0.5는 줄 수 없다. 이렇게 된다면 8가지 색밖에 표현을 못한다. 0에서 1사이에 어떤 값을 표현할 수 있어야 된다. 연속적인 값을 주기 위해서는 PWM을 사용한다. 이산적인 값을 사용해서 연속적인 값을 만들기 위해서 PWM을 사용한다.

### RGB_led_pwm.py

```py
import RPi.GPIO as GPIO
import signal
import sys
import time

def signal_handler(signal, frame):
    print("process stop")
    GPIO.cleanup()
    sys.exit(0)

signal.signal(signal.SIGINT, signal_handler)

RGBLEDPOWER = 19
GPIO.setmode(GPIO.BCM)

# RGB -> 432 번호 순임.
RED = 4
GREEN = 3
BLUE = 2

# GPIO setup
GPIO.setup(RGBLEDPOWER, GPIO.OUT)
GPIO.setup(RED, GPIO.OUT)
GPIO.setup(GREEN, GPIO.OUT)
GPIO.setup(BLUE, GPIO.OUT)

# PWM PWM 인스턴스 만들기
PWM_RED = GPIO.PWM(RED, 500) # 주파수가 500Hz
PWM_RED.start(100) # 100%로 시작
PWM_GREEN = GPIO.PWM(GREEN, 500)
PWM_GREEN.start(100)
PWM_BLUE = GPIO.PWM(BLUE, 500)
PWM_BLUE.start(100)

def setRGB(r, g, b):
    # 100%로 출력되는 비중(r, g, b값이 커질수록)이 커질수록 해당 불빛이 밝아진다.
    PWM_RED.ChangeDutyCycle(r)
    PWM_GREEN.ChangeDutyCycle(g)
    PWM_BLUE.ChangeDutyCycle(b)

while True:
    print("RGB LED Various Color")

    GPIO.output(RGBLEDPOWER, 1)

    for i in range(0, 26):
        for j in range(0, 26):
            for k in range(0, 26):
                setRGB(i * 4, j * 4, k * 4)
                time.sleep(0.05)
                print("R:%d G:%d B%d" %(i * 10, j * 10, k * 10))
```

삼중 포문이긴 한데, 처음에 i, j, k는 0 -> 처음에는 검정색 그 다음에 루프로 돌면 k가 1로 바뀌면서 4가 된다. 여튼 4의 배수만큼 돌다가 100%로 이동을 한다. 처음에는 파란색이 강조가 되다가 그 다음에는 초록 파랑이 섞여 -> 그 다음에는 마지막에 빨간색까지 같이 섞인거 색깔이 표현이 된다.

### rainbow.py

```py
import RPi.GPIO as GPIO
import signal
import sys
import time

def signal_handler(signal, frame):
    print("process stop")
    GPIO.cleanup()
    sys.exit(0)

signal.signal(signal.SIGINT, signal_handler)

RGBLEDPOWER = 19
GPIO.setmode(GPIO.BCM)

RED = 4
GREEN = 3
BLUE = 2

# GPIO setup
GPIO.setup(RGBLEDPOWER, GPIO.OUT)
GPIO.setup(RED, GPIO.OUT)
GPIO.setup(GREEN, GPIO.OUT)
GPIO.setup(BLUE, GPIO.OUT)

# PWM setup
PWM_RED = GPIO.PWM(RED, 500) # 주파수가 500Hz
PWM_RED.start(100) # 100%로 시작
PWM_GREEN = GPIO.PWM(GREEN, 500)
PWM_GREEN.start(100)
PWM_BLUE = GPIO.PWM(BLUE, 500)
PWM_BLUE.start(100)

def setRGB(r, g, b):
    PWM_RED.ChangeDutyCycle(r)
    PWM_GREEN.ChangeDutyCycle(g)
    PWM_BLUE.ChangeDutyCycle(b)

while True:
    # 전압값이 달라짐으로써 색이 달라지는 것이고 이 세 개가 섞이면서 가시광선으로 보이는 것이다.
    setRGB(100, 0, 0) # red
    time.sleep(1)
    setRGB(100, 30, 0) # orange
    time.sleep(1)
    setRGB(100, 100, 0) # yellow
    time.sleep(1)
    setRGB(0, 100, 0) # green
    time.sleep(1)
    setRGB(0, 0, 100) # blue
    time.sleep(1)
    setRGB(0, 0, 50) # deep blue
    time.sleep(1)
    setRGB(30, 20, 30) # purple
    time.sleep(1)
```

## water_pump.py

```py
import RPi.GPIO as GPIO
import signal
import sys
import time

def signal_handler(signal, frame) :
    print('process stop')
    GPIO.cleanup()
    sys.exit(0)

signal.signal(signal.SIGINT, signal_handler)
PUMP = 5 #GPIO 5(Wpi : 21)
GPIO.setmode(GPIO.BCM) #BCM Mode
GPIO.setup(PUMP, GPIO.OUT)

while True :
    print("here - PUMP on")
    GPIO.output(PUMP, 1)
    time.sleep(2)

    print("here - PUMP off")
    GPIO.output(PUMP, 0)
    time.sleep(2)
```

## Fan.py

펜이란 워터 펌트 옆에 있는 펜을 말한다. 이를 통해서 선풍기처럼 돌릴 수 있다.

```py
import RPi.GPIO as GPIO
import signal
import sys
import time

def signal_handler(signal, frame) :
    print('process stop')
    GPIO.cleanup()
    sys.exit(0)

signal.signal(signal.SIGINT, signal_handler)
GPIO.setmode(GPIO.BCM) #BCM Mode

Fan = 6 #GPIO 5(Wpi : 21)
GPIO.setup(Fan, GPIO.OUT)
while True :
    print("here - Fan on")
    GPIO.output(Fan, 1)
    time.sleep(2)
    print("here - Fan off")
    GPIO.output(Fan, 0)
    time.sleep(2)
```

## GPIO - Servo Motor

로봇 팔, CNC 등의 공작 기계 위치 결정에 사용되는 정밀 모터로 정의한다. Servant 노예라는 의미의 단어에서 유래되어 Servo즉, 주인의 명령에 충실하게 동작하는 모터라는 뜻이다. <br>

**_특징_** <br>

- 빈번하게 변화하는 위치나 속도의 명령치에 대한 정밀 추종
- 급가속이나 급제동에 대하여 정확히 반응하도록 구조화되어있음
- 큰 회전력과 회전자의 관성 모멘트를 적어야 함.

### Servo_Motor.py

```py
import RPi.GPIO as GPIO
import signal
import sys
import time

def signal_handler(signal, frame) :
    print('process stop')
    PWM_RC.stop()
    GPIO.cleanup()
    sys.exit(0)

signal.signal(signal.SIGINT, signal_handler)
GPIO.setmode(GPIO.BCM) #BCM
RCSERVO = 23 #GPIO 23(Wpi : 4)

GPIO.setup(RCSERVO, GPIO.OUT)
PWM_RC=GPIO.PWM(RCSERVO, 100)
PWM_RC.start(7.5)

while True :
    print("here - RCMOTOR on")
    PWM_RC.ChangeDutyCycle(5)
    time.sleep(1)
    PWM_RC.ChangeDutyCycle(95)
    time.sleep(1)
```

- servo motor: 정밀 조절이 목적 얘는 23번으로 무조건 정확히 얼마만큼 움직일 것인지를 정해야 돌아간다.

- 서보 모터는 몇 퍼센트의 Duty Cycle을 주면 서보 모터에는 기어 위치가 정해져 있는데 그 위치로 가있게 되는 것이다. 5%의 위치로 이동했다가 95%의 위치로 이동한다.

## Motion Sensor

### 동작 원리

- Type 1: <br>

  인체 또는 동물에게서 발생하는 적외선 감지(파장 약 10um 정도) <br>

  적외선 -> 전압 형태로 변환

- Type 2: <br>

  적외선 소스에서 발사한 신호가 반사되어 수신되는 신호를 감지하는 방식 <br>

  거리 정보까지도 측정이 가능. (가까이 있을 때는 멀리 찍히고 멀리 있을 때는 가까이 찍히는 것을 알 수 있다. 이 거리의 차이를 통해서 최환할 수 있다.)

### PLR_Sensor.py

GPIO에서 이벤트를 받는 함수이다. rising이란 0->1로 신호가 변하는 애가 rising, 1->0은 falling이다. 평소에는 low가 걸려있다가 어느 순간 detect가 되어서 0->1이 될때를 감지해서 그때 callback을 보내라. 27번에 신호가 왔다는 것은 지나갔다는 것이므로 별도의 쓰레드에게 시켜서 알아낸다.

```py
GPIO.add_event_detect(MOTION_IN, GPIO.RISING, callback=my_callback)
```

<br>

#### 🌟 이벤트 처리 + 인터럽트 처리 예시

전체 코드 ⏬

```py
import RPi.GPIO as GPIO
import signal
import sys
import time

counter = 0

def signal_handler(signal, frame):
    print("process stop")
    GPIO.cleanup()
    sys.exit(0)

# 카운터 값을 하나 증가해준다.
def my_callback(channel):
    global eventCounter
    eventCounter += 1
    global humandetect
    humandetect = 1

signal.signal(signal.SIGINT, signal_handler)

GPIO.setmode(GPIO.BCM)
# PIR 센서, 그 핀으로부터 정보를 받을 것이므로 in으로 쓴다.
MOTION_IN = 27
eventCounter = 0
humandetect = 0

GPIO.setup(MOTION_IN, GPIO.IN)

# 이벤트 처리
GPIO.add_event_detect(MOTION_IN, GPIO.RISING, callback=my_callback)

while True:
    if humandetect == 1:
        print("Detect %d" %eventCounter)
        humandetect = 0
        while GPIO.input(MOTION_IN):
            counter += 1
            print("high %d " %counter)
            time.sleep(1)
        counter = 0
    else:
        print("No detect")
    time.sleep(0.5)
```

- humandetect: 0이면 감지하지 못함. 1이면 감지함.

### PIR_Sensor2.py

0.1초마다 루프 반복 <br>

-> 모션이 들어왔는지 아닌지 내가 직접 읽어 <br>

-> 그래서 이거를 신호가 올 때까지 기다리냐, 내가 주기적으로 검사하냐에 따라 다른데 주기적으로 검사를 하는 애가 아래 코드에 속한다. 앞에 코드는 이벤트 방식이라고 하고, add_event_detect는 등록만 했지 실제로 도는 코드가 없으므로 별도의 쓰레드라는 것을 알 수 있다. 이벤트가 발생을 하면 이 함수를 호출한다. <br>

근데 이 코드는 계속 호출한다. 주기적으로 확인하는 방법이 polling이다. <br>

결과는 같을 수 있으나 두개는 정반대 방식이다.

```py
def loop():
    cnt = 0
    while True:
        if (GPIO.input(motion_in) == True):
            print("Detected %d" %cnt)
            cnt += 1
        time.sleep(0.1)
```

```py
import RPi.GPIO as GPIO
import time

motion_in = 27

GPIO.setmode(GPIO.BCM)
# 신호가 와야 되므로 GPIO.IN을 사용.
GPIO.setup(motion_in, GPIO.IN)

def loop():
    cnt = 0
    while True:
        if (GPIO.input(motion_in) == True):
            print("Detected %d" %cnt)
            cnt += 1
        time.sleep(0.1)

try:
    loop()
except KeyboardInterrupt:
    print("Sensing is terminated....!")
    pass
finally:
    GPIO.cleanup()
```

## Ultrasonic Sensor

### 동작 원리

초음파 신호를 전송하여 반사되는 신호를 수신하여 시간적으로 계산해 준다. 거리 측정에 주로 활용된다.

![다운로드](https://user-images.githubusercontent.com/96654391/196374984-f9f15c76-c08e-47f2-9fb3-5b4e68ded869.jpg) <br>

이렇게 생겼는데 한쪽은 TX(transmit), 다른 한쪽은 RX(receive)라고 부른다. <br>

그래서 TX 부분에서 40kHz 속도로 음파를 내보냈을 때, 물체에 의해서 반사되는 음파를 RX가 인지를 한다. 음파를 보내는 속도도 알기 때문에 이를 통해서 물체까지의 거리를 구할 수 있다는 것이다. <br>

정확한 거리를 계산하기 위해서 TX가 보낸 음파가 RX로 와야된다. RX에 다른 음파가 온 것으로 거리 계산을 하면 안되기 때문에. 따라서 최대 거리의 장애물에서 오는 시간 차가 있기 때문에 TX보다 RX는 늦게 감흥이 된다. RX가 켜지고 오는 어떤 주파수라도 TX가 보냄을 가정하고 인지를 하게 된다. <br>
<br>

### Ultrasonic_Sensor.py

위에서 말했던 TX를 TRIGGER로서 변수를 잡았고 핀 번호는 18번이다. <br>

RX는 EXHO로서 변수를 잡았고 핀 번호는 21번이다. <br>
<br>

여기서 TX를 잠깐 켰다가 끄고,

```py
# 먼저 트리거 핀을 OFF 상태로 유지한다.
GPIO.output(GPIO_TRIGGER, False)
time.sleep(2)

# TX를 0.00001초 켰다가
GPIO.output(GPIO_TRIGGER, True)
time.sleep(0.00001)
# 끈다.
GPIO.output(GPIO_TRIGGER, False)
```

그 다음 RX에 오는 주파수를 감지한다고 했다.

```py
# 에코핀이 ON되는 시점을 시작 시간으로 잡는다.
while GPIO.input(GPIO_ECHO) == 0:
    start = time.time()

# 에코 핀이 다시 OFF되는 시점을 반사파 수신 시간으로 잡는다.
while GPIO.input(GPIO_ECHO) == 1:
    stop = time.time()
```

<br>

전체 코드 ⏬

```py
import time
import RPi.GPIO as GPIO

# 핀 넘버링을 BCM 방식을 사용한다.
GPIO.setmode(GPIO.BCM)

# HC-SR04의 트리거 핀을 GPIO 18번, 에코핀을 GPIO 21에 연결한다.
GPIO_TRIGGER = 18
GPIO_ECHO = 21

print("Ultrasonic Distance Measurement")

# 초음파를 내보낼 트리거 핀은 출력 모드로, 반사파를 수식할 에코 핀은 입력 모드로 설정한다.
GPIO.setup(GPIO_TRIGGER, GPIO.OUT)
GPIO.setup(GPIO_ECHO, GPIO.IN)

try:
    while True:
        stop = 0
        start = 0
        # 먼저 트리거 핀을 OFF 상태로 유지한다.
        GPIO.output(GPIO_TRIGGER, False)
        time.sleep(2)

        # 10us 펄스를 내보낸다.
        # 주파수릐 속도가 40키로헤르츠
        # 파이썬에서 이 펄스는 실체 100us 근처가 될 것이다.
        # 하지만 HC-SR04 센서는 이 오차를 받아준다.
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

        # 초음파는 반사파이기 때문에 실제 이동거리는 2배이다 따라서 .2로 나눈다.
        # 음속은 편의상 340m/s로 계산하낟. 현재 온도를 반영해서 보정할 수 있다.
        if (stop and start):
            distance = (elapsed * 34000.0) / 2
            print("Distance: %.1f cm" %distance)
except KeyboardInterrupt:
    print("Ultrasoic Distance Measurement End")
    GPIO.cleanup()

# Reset GPIO settings
GPIO.cleanup()
```

### Ultrasonic_Sensor2.py

```py
import RPi.GPIO as GPIO
import time

GPIO.setmode(GPIO.BCM)

# 거리를 제는개 아니르 트리거에 온이 되는 순간부터 오프가 되는 순간까지의 거리를 구하는 것이다.
trig = 18
echo = 21

print("start")

GPIO.setup(trig, GPIO.OUT)
GPIO.setup(echo, GPIO.IN)

try:
    while True:
        GPIO.output(trig, False)
        time.sleep(0.5)

        GPIO.output(trig, True)
        time.sleep(0.00001)
        GPIO.output(trig, False)

        while GPIO.input(echo) == 0:
            pulse_start = time.time()
            print("hello1")
        while GPIO.input(echo) == 1:
            pulse_end = time.time()
            print("hello2")
        pulse_duration = pulse_end - pulse_start
        distance = pulse_duration * 17000
        distance = round(distance, 2)

        print("Distance: ", distance, "cm")

except KeyboardInterrupt:
    GPIO.cleanup()
```

### Ultrasonic_Sensor3.py

```py
import RPi.GPIO as GPIO
import time
# GPIO Mode (BOARD / BCM)
GPIO.setmode(GPIO.BCM)

# set GPIO Pins
GPIO_TRIGGER = 18
GPIO_ECHO = 21

# set GPIO direction (IN / OUT)
GPIO.setup(GPIO_TRIGGER, GPIO.OUT)
GPIO.setup(GPIO_ECHO, GPIO.IN, pull_up_down = GPIO.PUD_UP)

def distance():
    # set Trigger to HIGH
    GPIO.output(GPIO_TRIGGER, True)

    # set Trigger after 0.01ms to LOW
    time.sleep(0.00001)
    GPIO.output(GPIO_TRIGGER, False)
    StartTime = time.time()
    StopTime = time.time()

    # save StartTime
    while GPIO.input(GPIO_ECHO) == 0:
        startTime = time.time()

    # save time of arrival
    while GPIO.input(GPIO_ECHO) == 1:
        StopTime = time.time()

    # time difference between start and arrival
    TimeElapsed = StopTime - StartTime

    # multiply with the sonic speed (34300 cm/s)
    # and dive by 2 becase there and back
    distance = (TimeElapsed * 34300) / 2

    return distance

if __name__ == '__main__':
    try:
        while True:
            dist = distance()
            print("Measured Distance = %.1f cm" %dist)
            time.sleep(1)

    # Reset by pressing CTRL + C
    except KeyboardInterrupt:
        print("Measurement stopped by User")
        GPIO.cleanup()
```
