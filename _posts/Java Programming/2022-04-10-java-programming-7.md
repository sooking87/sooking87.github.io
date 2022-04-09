---
title: "[chap 9] 자바 GUI 기초, AWT와 Swing"
excerpt: "[chap 9] 자바 GUI 기초, AWT와 Swing"
categories: [Java Programming]
tags: [Java Programming, Java]
toc: true
toc_sticky: true
---

## 🔮 자바 GUI 패키지

### 📍 GUI 패키지 계층 구조

모든 GUI(AWT, Swing)은 _Componet_ 클래스를 반드시 상속받으며, 스윙 컴포넌트의 클래스 명은 모두 J로 시작한다. AWT 컴포넌트는 Button, Label 등과 같이 Component를 직접 상속받는 것들과 Panel, Frame 등과 같이 Container를 상속받는 것이 있다. JApplet, JFrame, JDialog를 제외한 모든 스윙 컴포넌트들은 JComponent를 상속받는다.
<br>

- Component Class
  - Container Class
    - Windows Class
      - Frame Class
      - Dialog Class
    - Panel Class
    - ScrollPane Class
  - Button Class
  - Canvas Class
  - Checkbox Class
  - Choice Class
  - Label Class
  - List Class
  - Scollbar Class
  - TextComponent Class
    - TextArea
    - TextField
- MenuComponent Class
  - MenuItem Class
    - CheckboxMenuItemt Class
    - Menu Class
  - Menubar Class

### 📍 컨테이너와 컴포넌트

> 컨테이너 : 다른 컴포넌트를 포함할 수 있는 GUI 컴포넌트

- java.awt.Container를 상속받음.
  다른 컨테이너에 포함될 수 있다. <br>
- AWT 컨테이너 : Panel, Frame, Applet, Dialog, Window <br>
- Swing 컨테이너 : JPanel, JFrame, JApplet, JDialog, JWindow <br>

> 컴포넌트 : 컨테이너에 포함되어야 화면에 출력될 수 있는 GUI 객체. 컨테이너에 컴포넌트를 add 순서대로 그린다라고 생각하면 쉽다 <br>

다른 컴포넌트를 포함할 수 없는 순수 컴포넌트 <br>
모든 GUI 컴포넌트가 상속받는 클래스 : java.awt.Component <br>
스윙 컴포넌트가 상속받는 클래스 : java.swing.JComponent <br>

최상위 컨테이너 :
다른 컨테이너에 포함되지 않고도 화면에 출력되며 독립적으로 존재 가능한 컨테이너

- 스스로 화면에 자신을 출력하는 컨테이너 => JFrame, JDialog, JApplet
  <br>

예제에서 Button, Checkbox를 그리기 위해서 무조건 `f.setLayout(new FlowLayout());` 을 써주었다. 이걸 보면 Frame이 컨테이너, 그 안에 컴포넌트들이 있는 것을 알 수 있다.

## 🔮 컨테이너와 배치

컨테이너에 부착되는 컴포넌트들의 위치와 크기는 컨테이너 내부에 있는 배치관리자(Layout Manager)에 의해 결정된다.

**관계 1.** 컨테이너마다 배치관리자는 하나씩 있다. <br>

**관계 2.** 배치관리자는 컨테이너에 컴포넌트가 부착되는 시점에 컴포넌트의 위치와 크기를 결정한다. 컨테이너의 크기가 변하면 내부 컴포넌트들의 위치와 크기를 모두 재조절하여 재배치한다. <br>

### 📍 배치관리자의 종류

- FlowLayout : 컨테이너에 부착되는 순서를 _왼쪽에서 오른쪽으로_ 컴포넌트를 배치. 공간없으면 아래로 내려와서 다시 왼쪽에서 오른쪽으로 배치

- BorderLayout : 컨테이너의 공간을 동, 서, 남, 북, 중앙 **5개 영역** 으로 나누고 응용프로그램에서 지정한 영역에 컴포넌트를 배치 <small> 헐,,,,,,,,,,,,,HW 4이게 정답 아님,,,,,,? </small>

- GridLayout : 컨테이너의 공간을 응용프로그램에서 설정한 동일한 크기의 **2차원 격자** 로 나누고, 컴포넌트가 삽입되는 순서대로 _좌에서 우_ 로 다시 _위에서 아래_ 로 배치한다.

- CardLayout : **카드** 를 쌓아 놓은 듯이 컴포넌트를 포개어 배치. 컴포넌트의 크기는 컨테이너의 크기와 동일

| AWT와 스윙 컨테이너 | 디폴트 배치관리자 |
| :-----------------: | :---------------: |
|   Window, JWindow   |   BorderLayout    |
|    Frame, JFrame    |   BorderLayout    |
|   Dialog, JDialog   |   BorderLayout    |
|    Panel, JPanel    |     FlowLaout     |
|   Applet, JApplet   |    FlowLayout     |

<br>

> ❓ 배치관리자 맘대로 설정하려면? -> _setLayout()_ 메소드 호출,,,

```java
Container.setLayout(new BorderLayout);
```

#### FlowLayout 배치관리자

📐 부착 방법 : add(Component comp) <br>
컴포넌트를 왼 -> 오, 자리 없으면 밑으로 내려와서 다시 왼 -> 오. 근데 컨테이너의 크기가 변하면, FlowLayout 배치관리자에 의해 컨테이너의 크기에 맞도록 컴포넌트가 재배치된다.

- 생성자

  - _FlowLayout()_
  - _FlowLayout(int align)_
  - _FlowLayout(int align, int hGap, int vGap)_

- align: 컴포넌트의 정렬 방법. FlowLayout.LEFT, FlowLayout.RIGHT, FlowLayout.CENTER(디폴트)
- hGap : 좌우 컴포넌트 사이의 수평 간격, 픽셀 단위, 디폴트 5
- vGap : 상하 컴포넌트 사이의 수직 간격, 픽셀 단위, 디폴트 5
  ```java
  //ex
  new FlowLayout();
  new FlowLayout(FlowLayout.LEFT);
  new FlowLayout(FlowLayout.LEFT, 10, 20);
  ```

#### BorderLayout 배치관리자

📐 부착 방법 : add(Component comp, int index) <br>

- comp : 컨테이너에 부착되는 컴포넌트
- index : BorderLayout.EAST, BorderLayout.WEST, BorderLayout.SOUTH, BorderLayout.NORTH, BorderLayout.CENTER

컨테이너의 크기가 변하면 BorderLayout 역시 새로운 크기에 맞도록 컴포넌트의 크기를 재조종한다. BorderLayout 배치관리자를 사용하는 컨테이너에는 일차적으로 5개의 컴포넌트밖에 붙힐 수 없다. 5개 이상을 붙히고자한다면, 한 영역에 JPanel 등 다른 컨테이너를 부착하고 이곳에 컴포넌트를 부착하면 된다.

- 생성자

  - _BorderLayout()_
  - _BorderLayout(int hGap, int vGap)_

- hGap : 좌우 컴포넌트 사이의 수평 간격, 픽셀 단위, 디폴트 0
- vGap : 상하 컴포넌트 사이의 수직 간격, 픽셀 단위, 디폴트 0 <br>
  생성자에서 이미 위치를 지정해 놓았으므로 align은 필요 없다.
  ```java
  //ex
  new BorderLayout();
  new BorderLayout(10, 20);
  ```

#### GridLayout 배치관리자

📐 부착 방법 : add(Component comp) <br>

- 생성자

  - _GridLayout()_
  - _GridLayout(int rows, int cols)_
  - _GridLayout(int rows, int cols, int hGap, int vGap)_

- rows : 그리드의 행 수, 디폴트 1
- cols : 그리드의 열 수, 디폴트 1
- hGap : 좌우 컴포넌트 사이의 수평 간격, 픽셀 단위. 디폴트 0
- vGap : 상하 컴포넌트 사이의 수직 간격, 픽셀 단위. 디폴트 0
  <br>

📌 컨테이너가 커져도 위치 동일,,,하게 하는 방법!!! 이거다,,,,,,이거야,,,,!!!!!!!!!!!!!!!!!!!!!!!!! <small> 아닌감,,? </small>

#### 배치관리자가 없는 컨테이너

배치관리자는 컴포넌트를 절대적인 위치에 배치하지 않고, 다른 컴포넌트의 오르녹이나 아래와 같이 상대적인 위치에 배치한다. **그러므로 컨테이너의 크기가 변하면 컴포넌트의 위치도 함꼐 변한다.**

📌 배치관리자를 없애야되나,,,?

- 컨테이너의 배치관리자 제거 <br>
  `container.setLayout(null);`

- 📌 컴포넌트의 절대 위치와 절대 크기 설정 <br>

배치관리자를 제거하게 되면 모든 컴포넌트들의 값이 0이 되기 때문에 절대 위치와 절대 크기의 설정이 필요하다. <br>

_void setSize(int width, int height)_ <br>
_void setLovation(int x, int y)_ <br>
_void setBounds(int x, int y, int width, int height)_ <br>
