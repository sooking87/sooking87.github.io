---
title: "[chap 11] 기본적인 스윙 컴포넌트와 활용"
excerpt: "[chap 11] 기본적인 스윙 컴포넌트와 활용"
categories: [Java Programming]
tags: [Java Programming, Java]
toc: true
toc_sticky: true
---

## 🔮 스윙 컴포넌트

스윙 프로그램으로 구성된 GUI 화면 구성 방법 <br>
1. 컴포넌트 기반 GUI 프로그래밍 -> chap 11.
2. 그래픽 기반 GUI 프로그래밍 -> chap 12.
<br>

### 📍 JComponent 클래스

JComponent는 스윙이 가지고 있는 공통 메소드와 상수를 모두 포함하고 있다. 따라서 🌟 중요함!<br>

### 📍 컴포넌트의 모양과 관련된 메소드

- setForeground(Color) : 글자색 설정
- setBackground(Color) : 배경색 설정
- setOpaque(boolean) : 불투명성 설정
- setFont(Font) : 폰트 설정
- getFont() : 폰트 리턴

### 📍 컴포넌트의 상태와 관련된 메소드

- setEnabled(boolean) : 컴포넌트 활성화/비활성화
- setVisible(boolean) : 컴포넌트 보이기/숨기기
- isVisible() : 컴포넌트의 보이는 상태 리턴

### 📍 컴포넌트의 위치와 크기에 관련된 메소드

- getWidth()
- getHeight()
- getX()
- getY()
- getLocationOnScreen()
- setLocation(int, int)
- setSize(int, int)

### 📍 컨테이너를 위한 메소드

- add(Component comp)
- remove(Component comp)
- removeAll()
- getComponents() : 자식 컴포넌트 배열 리턴
- getParent() : 부모 컨테이너 리턴
- getTopLevelAncestor() : 최상위 부모 컨테이너 리턴

## 🔮 JLabel

이미지나 문자열을 스크린에 출력하는 레이블 컴포넌트를 만드는 클래스이다. 

- 생성자
    - JLabel()
    - JLabel(Icon img)
    - JLabel(String text)
    - JLabel(String text, Icon img, int hAlign) -> hAlign : SwingConstantes.LEFT, SwingConstantes.RIGHT, SwingConstants.CENTER

## 🔮 JButton

- 생성자
    - JButton()
    - JButton(Icon img)
    - JButton(String text)
    - JButton(String text, Icon img)

이미지 버튼 만드는 방법 : ImageIcon 을 만들고, 이미지를 읽어와서 버튼 컴포넌트에 붙혀 넣는다. 

```java
ImageIcon normalIcon = new ImgaeIcon("./images.dog.png");
ImageIcon rolloverIcon = new ImgaeIcon("./images.dog.png");
ImageIcon pressedIcon = new ImgaeIcon("./images.dog.png");

JButton button = new JButton("test Button", normalIcon);
button.setRolloverIcon(rolloverIcon);
button.setPressedIcon(pressedIcon);
```
