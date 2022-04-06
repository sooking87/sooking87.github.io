---
title: "[chap 5] 상속"
excerpt: "[chap 5] 상속"
categories: [Java Programming]
tags: [Java Programming, Java]
toc: true
toc_sticky: true
---

❗ 모든 내용 업로드 X

## 🔮 상속

상속이라는 개념을 통해서 다양한 추가적인 개념이 생긴다. 상속으로 인해서 코드 중복을 제거하고 클래스를 간결하게 한다.
서브 클래스는 슈퍼 클래스 + 서브 클래스 추가 멤버가 된다.

### 📍 상속의 특징

1. 클래스의 다중 상속을 지원하지 않는다.
2. 상속의 획수에 제한을 두지 않는다.
3. 최상위에 java.lang.Object 클래스가 있다.

### 📍 상속에서의 접근 지정자

- 슈퍼 클래스의 private 멤버
  서브 클래스 포함하여 **어떤 클래스도 접근 불가**
- 슈퍼 클래스의 디폴트 멤버
  **패키지 내에 모든 클래스 접근 가능**
- 슈퍼 클래스의 public 멤버
  **모든 패키지 내에서 접근 가능**
- 슈퍼 클래스의 protected 멤버
  - 같은 패키지인 경우
    **모든 클래스 사용 가능**
  - 다른 패키지인 경우
    **접근 불가**

### 📍 상속과 생성자 -> super() (졸 중요)

- 서브 클래스의 생성자를 호출 -> 자동적으로 슈퍼 클래스의 기본 생성자 호출
- 서브 클래스의 생성자에서 super()를 통해서 슈퍼 클래스에서 호출될 생성자를 선택할 수 있음. super()는 슈퍼 클래스 생성자를 호출하는 코드이다.

1. main -> 서브 클래스 생성자 호출
   ```java
   Student Sohn = new Student("SohnSooKyoung", 21, 165, 2116313);
   ```
2. 서브 클래스 생성자 -> super()을 통해서 슈퍼 클래스 생성자 호출

   ```java
   public Student2(String name, int age, int height, int studentID) {
       this(name, age, height, "Student", 2116313);
   }

   public Student2(String name, int age, int height, String career, int studentID) {
       super(name, age, height, career);
       this.studentID = studentID;
   }
   ```

   this() 메소드를 통해서 같은 클래스 내의 생성자 호출 -> 그 생성자에서 String, int, int, String을 매개변수로 가지는 생성자 호출

3. 슈퍼 클래스 생성자 실행
   ```java
   public Human(String name, int age, int height, String career) {
       this.name = name;
       this.age = age;
       this.height = height;
       this.career = career;
   }
   ```
   슈퍼 클래스 생성자에서 일부 초기화
4. 서브 클래스 생성자 실행
5. main에서 객체 생성, 멤버 초기화 완료!

## 🔮 캐스팅

캐스팅이란 타입 변환을 말한다.

### 📍 업캐스팅

`Human Sohn = new Student();` <br>
와 같이 객체를 지칭하는 레퍼런스 변수의 타입과 객체의 타입이 다른 경우를 말한다. 업캐스팅을 하게 된다면 Sohn 객체는 Human 타입이므로 Human.java에서 정의한 멤버만 사용할 수 있다. 여기서 **다형성** 이라는 개념이 적용된다.

- 다형성
  다형성이란 형이 많다라는 뜻으로, 자바는 다양한 형을 커버할 수 있다는 뜻이다.
  1. 여러 가지 형태를 가질 수 있는 것.
  2. 하나의 메소드나 클래스가 있을 때 이것들이 다양한 방법으로 동작하는 것(오버 로딩, 오버라이딩)
  3. 하나의 참조변수로 여러 타입의 객체를 참조할 수 있는 것(업캐스팅, (이론상)다운캐스팅)

### 📍 다운캐스팅

```java
Human Sohn = new Student();
Student s = (Student)Sohn;
```

이렇게 하면 이론상 가능은 하나, 명시적 형 변환이 필요

### 📍 instanceof
