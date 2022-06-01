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