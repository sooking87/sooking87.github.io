---
title: "[Term? Project] 그래픽스에 이벤트 리스너 등록하기"
excerpt: "[Term Project] 그래픽스에 이벤트 리스너 등록하기"
categories: [Java Programming]
tags: [Java Programming, Java]
toc: true
toc_sticky: true
---

```java
package Chap12;

import java.awt.*;
import javax.swing.*;
import java.awt.event.*;

public class NO_5ControlImageSize {
    private JFrame jf = new JFrame();
    private MyPanel panel = new MyPanel();

    public NO_5ControlImageSize() {
        jf.setTitle("그래믹 이미지 혹대 축소 연습");
        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jf.setContentPane(panel);

        jf.setSize(500, 500);
        jf.setVisible(true);

        panel.setFocusable(true);
        panel.requestFocus();
    }

    class MyPanel extends JPanel {
        private ImageIcon icon = new ImageIcon("./images/dog5.png");
        private Image img = icon.getImage();
        int width = 50;
        int height = 50;

        public void paintComponent(Graphics g) {
            super.paintComponent(g);

            // MyPanel에 키 리스너 등록
            // 익명 클래스 사용 이유? : 이벤트를 통해서 변경되는 값을 Graphics g를 사용하여 윈도우에 그려야되기 때문에
            this.addKeyListener(new KeyAdapter() {
                public void keyPressed(KeyEvent e) {
                    int keyChar = e.getKeyChar();
                    if (keyChar == '+') {
                        width = (int) (width * 1.1);
                        height = (int) (height * 1.1);

                    } else if (keyChar == '-') {
                        width = (int) (width * 0.9);
                        height = (int) (height * 0.9);
                    }
                    repaint(); // 컴포넌트의 모양, 텍스트, 크기, 색 등을 변경하는 경우, 변경 사항을 윈도우에 그리기 위해 호출 필요
                }
            });
            g.drawImage(img, 10, 10, width, height, this); // 원본 크기로 그리라고 했는데, 원본 크기가 넘 커서 50, 50으로 그렸어요!

        }
    }

    public static void main(String[] args) {
        new NO_5ControlImageSize();
    }
}
```
```java
package Chap12;

import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class NO_2backgroundImage {
    private MyPanel panel = new MyPanel();
    private JFrame jf = new JFrame();

    // 생성자
    public NO_2backgroundImage() {
        jf.setTitle("NO.2");
        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jf.setContentPane(panel);

        jf.setSize(500, 500);
        jf.setVisible(true);
    }

    class MyPanel extends JPanel {
        private ImageIcon icon = new ImageIcon("./images/dog4.png");
        private Image img = icon.getImage();
        int x, y;

        public void paintComponent(Graphics g) {
            super.paintComponent(g); // super = JPanel, paintComponent -> 이거 없으면 안그려짐

            g.drawImage(img, 0, 0, getWidth(), getHeight(), this);

            // MyPanel에 마우스 리스너 등록
            // MouseAdapter : 필요한 메소드만 오버라이딩 가능
            // 익명 클래스 사용 이유? : 이벤트를 통해서 변경되는 값을 Graphics g를 사용하여 윈도우에 그려야되기 때문에 + 간편
            this.addMouseMotionListener(new MouseAdapter() {
                public void mouseDragged(MouseEvent e) {
                    x = e.getX();
                    y = e.getY();
                    repaint(); // 컴포넌트의 모양, 텍스트, 크기, 색 등을 변경하는 경우, 변경 사항을 윈도우에 그리기 위해 호출 필요
                }
            });
            g.setColor(Color.GREEN);
            g.fillOval(x, y, 20, 20);
            // 원은 마우스가 가리키는 x, y에 그려져야된다.

        }
    }

    public static void main(String[] args) {
        new NO_2backgroundImage();
    }
}
```
```java
package Week12;

import java.awt.*;
import java.awt.Graphics;
import java.awt.event.*;
import javax.swing.*;

public class ButtonEventType2 extends JPanel implements ActionListener {
    boolean flag = false;
    private int light = 0;

    public ButtonEventType2() {
        setLayout(new BorderLayout());
        setVisible(true);
        setSize(getPreferredSize());

        JButton b = new JButton("traffic light");
        b.addActionListener(this);
        add(b, BorderLayout.SOUTH);
    }

    protected void paintComponent(Graphics g) {
        super.paintComponent(g);

        // 빨, 녹, 노 신호등을 만듬
        g.setColor(Color.BLACK);
        g.drawOval(100, 100, 100, 100);
        g.drawOval(100, 200, 100, 100);
        g.drawOval(100, 300, 100, 100);

        // light가 0이면
        if (light == 0) {
            g.setColor(Color.RED);
            g.fillOval(100, 100, 100, 100);
        }
        // light가 1이면
        else if (light == 1) {
            g.setColor(Color.GREEN);
            g.fillOval(100, 200, 100, 100);
        }
        // light가 2이면
        else {
            g.setColor(Color.ORANGE);
            g.fillOval(100, 300, 100, 100);
        }
    }

    public void actionPerformed(ActionEvent arg0) {
        if (++light >= 3) // 만약 1이 더해진 light가 3이상이라면
            light = 0; // 0부터 다시 시작
        repaint();
    }
}
```