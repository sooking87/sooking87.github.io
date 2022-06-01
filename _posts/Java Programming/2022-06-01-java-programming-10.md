---
title: "[Term? Project] 라벨 내에서 이미지 밑에 라벨 붙히기"
excerpt: "[Term Project] 라벨 내에서 이미지 밑에 라벨 붙히기"
categories: [Java Programming]
tags: [Java Programming, Java]
toc: true
toc_sticky: true
---

```java

package TERMPROJECT;

import java.awt.FlowLayout;
import javax.swing.JFrame; // 윈도우
import javax.swing.JLabel; // 문자열 출력
import javax.swing.SwingConstants; // 속성을 정의하기위한 상수 집합
import javax.swing.Icon; // 아이콘
import javax.swing.ImageIcon; // 이미지 아이콘

class test extends JFrame {
    private static final long serialVersionUID = 1L;
    private JLabel label1;
    private JLabel label2;
    private JLabel label3;

    public test() {
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setTitle("JLabel 테스트"); // 제목 표시줄 표시 문자열
        setLayout(new FlowLayout()); // Layout 지정

        Icon scope = new ImageIcon("C:\\STUDY\\3학기\\전공\\--\\src\\Images\\coffee\\americano.png");
        label3 = new JLabel();
        label3.setText("레이블 3");
        label3.setIcon(scope);
        label3.setHorizontalTextPosition(SwingConstants.CENTER);
        label3.setVerticalTextPosition(SwingConstants.BOTTOM);
        label3.setToolTipText("레이블3");
        add(label3);

        setSize(300, 300);
        setVisible(true);
    }

    public static void main(String[] args) {
        new test();
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