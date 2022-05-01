---
title: "[chap 10] 자바의 이벤트 처리"
excerpt: "[chap 10] 자바의 이벤트 처리"
categories: [Java Programming]
tags: [Java Programming, Java]
toc: true
toc_sticky: true
---

## 🔮 이벤트 기반 프로그래밍

이벤트 기반 프로그래밍이랑 이벤트의 발생에 의해 프로그램 실행 흐름이 결정되는 방식의 프로그래밍 패러다임이다. 이벤트란 키 입력, 마우스 클랙, 드래그 등 사용자의 액션이나 센서 등 외부 장치로부터의 입력, 네트워크를 통한 데이터 수신 등에 의해서 발생한다.

### 📍 실행 과정

1. 버튼 클릭 -> new 이벤트 발생
2. 이벤트는 마우스 드라이버를 거쳐 JVM에 전달
3. JVM은 **이벤트 분배 스레드** 에게 마우스 클릭에 관한 정보 전송
4. 이벤트 분배 스레드는 **이벤트 객체(ActionEvent)** 를 생성, 이벤트 객체에는 전송되는 여러 정보를 가지고 있는데, 그 중 이벤트를 발생시킨 컴포넌트 정보를 **이벤트 소스** 라고 부른다.
5. 이벤트 분배 스레드는 해당 컴포넌트의 **이벤트 리스너** 를 찾아서 호출
6. 이벤트 리스너로부터 리턴 후 다음 이벤트를 기다린다.

![download3](https://user-images.githubusercontent.com/96654391/166133091-64ba6198-1370-4453-96b2-b224dace1eed.png) <br>
요런 느낌?

### 📍 용어 정리

- 이벤트 소스 : 이벤트를 발생시킨 GUI 컴포넌트
- 이벤트 객체 : 발생한 이벤트에 대한 정보를 담는 객체
- 이벤트 리스너 : 이벤트를 처리하는 코드로서 **컴포넌트에 등록** 되어야 작동 가능
- 이벤트 분배 스레드 : 무한 루프를 실행하는 스레드로 JVM으로부터 이벤트 발생을 통지받아 적절한 이벤트 객체를 생성하여 이에 맞는 이벤트 리스너를 찾아 호출

## 🔮 이벤트 객체

이벤트 객체란 현재 발생한 이벤트에 관한 정보를 가진 객체이며, 이벤트 리스너에게 전달된다.

![download3](https://user-images.githubusercontent.com/96654391/166133248-1680276f-960f-405d-b381-c38e16495124.png) <br>
위와 같은 계층 구조를 가지고 있다. 각 이벤트의 종류별로 사용할 수 있는 메소드가 차이가 있으므로 주의깊게 볼 것!

### 📍 이벤트 객체와 이벤트 소스

|    이벤트 객체     |    이벤트 소스    |                                                      이벤트가 발생하는 경우                                                      |
| :----------------: | :---------------: | :------------------------------------------------------------------------------------------------------------------------------: |
|    ActionEvent     |      JButton      |                                                 마우스나 <Enter> 키로 버튼 선택                                                  |
|                    |     JMenuItem     |                                                         메뉴 아이템 선택                                                         |
|                    |    JTextFiedld    |                                                  텍스트 입력 중 <Enter> 키 입력                                                  |
|     ItemEvent      |     JCheckBox     |                                                    체크 박스의 선택 혹은 해제                                                    |
|                    |   JRadioButton    |                                                라디오 버튼의 선택 상태가 변할 때                                                 |
|                    | JCheckBoxMenuItem |                                              체크박스 메뉴 아이템의 선택 혹은 해제                                               |
| ListSelectionEvent |       JList       |                                               리스트에서 선택된 아이템이 변경될 때                                               |
|      KeyEvent      |     Component     |                                              키가 눌러지거나 눌러진 키가 떼어질 때                                               |
|     MouseEvent     |     Component     |                                                    마우스 작동에 대한 핸들링                                                     |
|     FocusEvent     |     Component     |                                                컴포넌트가 포커스를 받거나 잃을 때                                                |
|    WindowEvent     |      Window       | 윈도우를 상속받는 모든 컴포넌트에 대해 윈도우 활성화, 비활성화, 아이콘화, 아이콘에서 복구, 윈도우 열기, 윈도우 닫기, 윈도우 종료 |
|  AdjustmentEvent   |    JScrollBar     |                                                       스크롤바를 움직일 때                                                       |
|   ComponentEvent   |     Component     |                                      컴포넌트가 사라지거나, 나타나거나, 이동, 크기 변경 시                                       |
|   ContainerEvent   |     Container     |                                              Container에 컴포넌트의 추가 혹은 삭제                                               |

## 🔮 이벤트 리스너

이벤트 리스너란 이벤트를 처리하는 자바 프로그램 코드로서 클래스로 만든다. JDK는 이벤트 리스너 인터페이스를 제공하며, 개발자는 이 인터페이스를 상속받고 추상 메소드를 모두 구현하여 이벤트 리스너를 작성한다.

![download3](https://user-images.githubusercontent.com/96654391/166134629-9b9b886f-27b5-413f-8096-da527cbbac03.png)

### 📍 이벤트 리스너 작성 과정

1. 이벤트와 이벤트 리스너 선택
2. 이벤트 리스너 클래스 작성 -> 독립된 클래스 or 내부 클래스 or 익명 클래스
3. 이벤트 리스너 등록

### 📍 독립된 클래스로 이벤트 리스너 작성

```java
//독립 클래스로 Action 이벤트 리스너 작성
package Chap10;

import java.awt.*;
import javax.swing.*;
import java.awt.event.*;

public class IndepClassListener extends JFrame {
    public IndepClassListener() {
        // 컨테이너 설정
        setTitle("Action Event Listener Exam");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        Container c = getContentPane();
        c.setLayout(new FlowLayout());

        // 버튼 생성, 컨테이너에 붙히기
        JButton btn = new JButton("Action");
        btn.addActionListener(new MyActionListener()); // 버튼에 actionListener를 달기
        c.add(btn);

        setSize(350, 150);
        setVisible(true);
    }

    public static void main(String[] args) {
        new IndepClassListener();
    }
}

// 독립된 클래스로 이벤트 리스너 작성
class MyActionListener implements ActionListener {
    public void actionPerformed(ActionEvent e) {
        JButton b = (JButton) e.getSource(); // 이벤트 소스를 알아내기
        if (b.getText().equals("Action")) { // 버튼의 문자열이 Action 인지를 비교
            b.setText("액션"); // 버튼의 문자열을 "액션"으로 변경
        } else {
            b.setText("Action");
        }
    }
}
```

### 📍 내부 클래스로 이벤트 리스너 작성

```java
package Chap10;

import java.awt.*;
import javax.swing.*;
import java.awt.event.*;

public class InnerClassListener extends JFrame {
    public InnerClassListener() {
        // 컨테이너 설정
        setTitle("Action Event Listener Exam");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        Container c = getContentPane();
        c.setLayout(new FlowLayout());

        // 버튼 생성, 컨테이너에 붙히기
        JButton btn = new JButton("Action");
        btn.addActionListener(new MyActionListener()); // 버튼에 actionListener를 달기
        c.add(btn);

        setSize(350, 150);
        setVisible(true);
    }

    // 내부 클래스로 Action 리스너 작성
    public class MyActionListener implements ActionListener {
        public void actionPerformed(ActionEvent e) {
            JButton b = (JButton) e.getSource();
            if (b.getText().equals("Action")) {
                b.setText("액션");
            } else {
                b.setText("Action");
            }

            InnerClassListener.this.setTitle(b.getText()); // 프레임의 타이틀에 버튼 문자열을 출력한다.
        }
    }

    public static void main(String[] args) {
        new InnerClassListener();
    }
}
```

### 📍 익명 클래스로 이벤트 리스너 작성

```java
package Chap10;

import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

public class AnonymousClassListener {
    JFrame jf;
    Container c;
    JButton btn;

    public AnonymousClassListener() {
        jf = new JFrame("Write Action Event Listener");
        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        c = jf.getContentPane();
        c.setLayout(new FlowLayout());
        btn = new JButton("Action");
        c.add(btn);

        //익명 클래스 작성
        btn.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                JButton b = (JButton) e.getSource();
                if (b.getText().equals("Action"))
                    b.setText("Ready");
                else
                    b.setText("Action");

                jf.setTitle(b.getText());
            }
        });

        jf.setSize(350, 150);
        jf.setVisible(true);
    }

    public static void main(String[] args) {
        new AnonymousClassListener();
    }
}
```

이벤트 리스너에 맞는 이벤트 객체와 이벤트 소스가 있다.

## 🔮 어댑터 클래스

헐,,,,,,,,,대박 !! 리스너 인터페이스를 상속받아 이벤트 리스너를 구현할 때, 리스너 인터페이스의 메소드를 모두 구현해야되는 부담이 있다. -> 책말내말,,,,ㄹㅇ,,,, 여튼 이런 부담을 줄여주기 위해서 제공하는 클래스가 **_어댑터 클래스_** 이다.
|리스너 인터페이스|대응하는 어댑터 클래스|
|:--:|:--:|
|ActionListener|없음|
|ItemListener|없음|
|KeyListener|KeyAdapter|
|MouseListener|MouseAdapter|
|MouseMotionListener|MouseMotionAdaptoer or MouseAdapter|
|FocuseListener|FocusAdapter|
|WindowListener|WindowAdapter|
|AdjustmentListener|없음|
|ComponentListener|ComponentAdapter|
ContainerListener|ContainerAdapter|
<br>

💡 예시

```java
package Chap10;

import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

public class MouseAdapterEx extends JFrame {
    private JLabel la = new JLabel("Hello");

    public MouseAdapterEx() {
        setTitle("Mouse Event Ex");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        Container c = getContentPane();
        c.addMouseListener(new MyMouseAdapter()); // 컨테이너팬에 Mouse 이벤트 리스너 달기

        c.setLayout(null);
        la.setSize(50, 20);
        la.setLocation(30, 30);
        c.add(la);

        setSize(250, 250);
        setVisible(true);
    }

    class MyMouseAdapter extends MouseAdapter {

        public void mousePressed(MouseEvent e) {
            int x = e.getX();
            int y = e.getY();
            la.setLocation(x, y);
        }
    }

    public static void main(String[] args) {
        new MouseAdapterEx();
    }
}
```
