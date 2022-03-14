---
title: "[chap 3] 3.5 메소드에서 배열 리턴 ~ 3.7 자바의 예외 처리"
excerpt: "[chap 3] 3.5 메소드에서 배열 리턴 ~ 3.7 자바의 예외 처리"
categories: [Java Programming]
tags: [Java Programming, Java]
toc: true
toc_sticky: true
---

:pushpin: 앞 장은 Do it Java를 통해서 숙지하였으므로 미숙하다고 생각되는 부분부터 진행하였습니다.

## ✨ 메소드에서 배열 리턴

### :book: 개념

```java
int[] makeArray() {
    int temp[] = new int[4];
    return temp;
}
```

메소드에서 어떤 배열이든지 리턴하면, 배열의 공간 전체가 아니라 **배열에 대한 레퍼런스만 리턴** 된다. 배열에 대한 레퍼런스만 받기 때문에 리턴 타입을 선언할 때 배열의 크기를 쓰지 않아도 된다.

### :bulb: 활용

```java
package chap3;

public class ReturnArray {
    static int[] makeArray() {
        int temp[] = new int[4];
        for (int i = 0; i < temp.length; i++) {
            temp[i] = i;
        }
        return temp;
    }

    public static void main(String[] args) {
        int intArray[];
        intArray = makeArray();
        for (int i = 0; i < intArray.length; i++) {
            System.out.print(intArray[i] + " ");
        }
        System.out.println();
    }
}
```

결국 배열을 리턴하는 메소드는 리턴 타입만 배열로 리턴은 변수처럼 하면 되는 것을 알 수 있다. 그 이유는 배열에 대한 레퍼런스만 리턴을 하기 때문이다.
<br>

## :sparkles: main() 메소드

### :book: main() 메소드의 특징

#### :balloon: public 속성

다른 클래스에서 메소드 접근이 가능하다. 자바 프로그램이 실행을 시작할 때 JVM에 의해 호출되어야 하므로 public 속성으로 선언되어야 한다.

#### :balloon: static 속성

자신을 포함하는 클래스의 객체가 생성되기 전에 JVM에 의해 호출되므로 static 속성으로 선언되어야 한다.

#### :balloon: void 타입

아무 것도 리턴되지 않기 때문에 main() 메소드를 끝내기 위해서 _return;_ 문을 사용하면 안된다.

#### :balloon: 문자열 배열이 매개변수로 전달

- main() 메서드도 역시 메서드이므로 매개변수 args에 값 전달이 가능하다.
- :book: 전달 방법 :

  - vscode :
    1. 터미널을 켠다.(꼭 해당 디렉토리로 이동해야된다 ❗)
    2. `java (클래스 이름).java <args 전달 값>` 을 입력한다.
  - ecilpse :
    1. 클래스를 우클한다.
    2. Run as > Run Configurations 클릭
    3. Arguments 클릭
    4. program arguments에 args에 전달할 값을 입력한다.

- :bulb: 활용

명령행 인자의 개수는 **args.length** 를 이용하여 알 수 있다. 나는 VSCode를 사용하고 있으므로 `java Calc.java 2 2.0 20.5 88.1`를 입력해 주었다.

```java
package chap3;

public class Calc {
    public static void main(String[] args) {
        double sum = 0.0;

        for (int i = 0; i < args.length; i++) {
            sum += Double.parseDouble(args[i]);
        }

        System.out.println(sum);
    }
}

>>> 입력값 : java Calc.java 2 2.0 20.5 88.1
>>> 출력값 : 112.6
```

<br>

## :sparkles: 자바의 예외 처리

### :book: 예외란?

- 컴파일러 에러 : 문법이 맞지 않는 경우 사전에 알아서 컴파일러에서 걸러진다.

- 실행 중에 발생하는 예외
  - 정수를 0으로 나누는 경우(_ArithmeticException_)
  - 배열의 크기에서 벗어난 경우(_ArrayIndexOutOfBoundsException_)
  - 존재하지 않는 파일을 읽으려고 하는 경우(_FileNotFoundException_)
  - 정수 입력을 기다리는 코드가 실행되고 있을 때, 사용자가 문자를 입력한 경우(_InputMismatchException_)

실행 중에 발생하는 예외의 경우는 **자바 플랫폼** 이 먼저 알게 되어 현재 실행 중인 **응용프로그램** 에서 예외를 전달한다. 이에 대처하는 코드가 없다면 자바 플랫폼은 응용프로그램을 곧바로 종료시킨다.

- 플랫폼이란?
  개발환경, 실행환경 등 어떠한 목적을 수행할 수 있는 환경을 말합니다.
- 개발 환경 : 이클립스, 안드로이드 스튜디오, 비쥬얼 스튜디오 등
  (소프트웨어)
- 실행 환경 : Windows, MAC 등 (하드웨어)

자바라는 언어는 애초에 플랫폼으로부터 독립적으로 설계어 자바 코드는 운영체제나 CPU 등 플랫폼에 상관없이 JVM만 있으면 어떤 컴퓨터에서든 동일하게 실행된다. **자바 플랫폼**이 독립적으로 실행이 가능하게 하는 것은 JVM과 바이트 코드 덕분이다. .java파일은 javac를 통해서 .class 파일이 생성되고(바이트 코드) 이 파일이 java(JVM)을 통해서 인터프리터 형식으로 실행된다.

### :book: 예외 처리, try-catch-finally 문

- 예외 처리 : 프로그램이 실행되는 도중 발생할 수 있는 예외에 대한 대응을 말한다.

#### :balloon: 예외 처리 사용

```java
try {
    (예외가 발생할 가능성이 있는 실행문)
}
catch (처리할 예외 타입 선언) {
    (예외 처리문)
}
finally {
    (예외 발생 여부와 상관없이 무조건 실행되는 문장)
}
```

catch문에서 예외 처리할 타입을 작성해야되는데, 처리하고자 하는 예외가 많다면 하나씩 작성해야 된다.

|     예외 타입(예외 클래스)     |                          예외 발생 경우                           |
| :----------------------------: | :---------------------------------------------------------------: |
|      ArithmeticException       |                     정수를 0으로 나눌 때 발생                     |
|      NullPointerException      |                  null 레퍼런스를 참조할 때 발생                   |
|       ClassCastException       |           변환할 수 없는 타입으로 객체를 변환할 때 발생           |
|        OutOfMemoryError        |                     메모리가 부족한 경우 발생                     |
| ArrayIndexOutOfBoundsException |                 배열의 범위를 벗어난 점근 시 발생                 |
|    IllegalArgumentException    |                     잘못된 인자 전달 시 발생                      |
|          IOException           |              입출력 동작 실패 또는 인터럽트 시 발생               |
|     NumberFormatException      | 문자열이 나타내는 숫자와 일치하지 않는 타입의 숫자로 변환 시 발생 |
|     InputMismatchException     |  입력받고자 하는 데이터 타입과 다른 타입이 입력되었을 경우 발생   |

#### :bulb: 활용

```java
package chap3;

public class IndexOutOfHandling {
    public static void main(String[] args) {
        int[] arr = new int[5];

        for (int i = 0; i < arr.length; i++) {
            arr[i] = i + 1;
        }
        try {
            arr[6] = 7; //여기서 에러 발생 -> catch문 수행
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println(e);
        }
        for (int i = 0; i < arr.length; i++) {
            System.out.println(arr[i]);
        }
    }
}

>>> 출력값
java.lang.ArrayIndexOutOfBoundsException: Index 6 out of bounds for length 5
1
2
3
4
5
```

- :book: 다중 catch 사용법

```java
//입력된 수 범위에서 100의 소인수 개수 세기
package chap3;

import java.util.Scanner;

public class MultiCatch {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] arr = new int[n];
        int temp = 100;
        int cnt = 0;
        for (int i = 0; i < n; i++) {
            arr[i] = i;
        }
        try {
            for (int i = 0; i < n; i++) {
                if (temp % arr[i] == 0) {
                    cnt++;
                }
            }
        } catch (ArithmeticException e) {
            System.out.println(e);
        } catch (Exception e) {
            System.out.println(e);
        }
        System.out.println(cnt);
    }
}

>>> 입력값
5
>>> 출력값
java.lang.ArithmeticException: / by zero
0
```

- ❗ 다중 catch() 문에서 주의 해야될 점

상위 예외 클래스(위쪽에 처리한 예외 클래스)가 하위 예외 클래스(아래쪽에 처리한 예외 클래스)보다 아래쪽에 위치해야된다. try 문에서 예외가 발생했다면 catch() 문을 위에서부터 차례대로 검색하게 된다.
