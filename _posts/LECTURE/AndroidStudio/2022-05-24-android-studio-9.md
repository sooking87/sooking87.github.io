---
title: "12.2주차"
excerpt: "12.2주차"
categories: [Android Studio]
tags: [Android Studio, Java]
toc: true
toc_sticky: true
---

# 메뉴와 대화상자

## 메뉴

- 옵션 메뉴 : 화면 오른쪽 위 메뉴 아이콘을 눌렀을 때, 화면에 나오는 메뉴, 목록이 많으면 스크롤 해서 사용
- 컨텍스트 메뉴 : 날짜를 롱클릭하면 나오며 제목과 함께 화면의 중앙에 출력된다.

### 옵션 메뉴를 사용하는 방법

메뉴 XML 파일 생성 후 Java에서 호출

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:id="@+id/baseLayout">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="오른쪽 위 메뉴를 누르세요."
        android:textSize="20dp"/>

    <Button
        android:id="@+id/button1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="이건 버튼" />

</LinearLayout>
```

### 메뉴 XML 파일을 이용한 방식

1. 메뉴 폴더 생성 및 메뉴 XML 파일 생성 -> 편집 -> _res > new > Android Resource Directory > Directory Name : Menu 선택 -> Menu 폴더에 우클 > menu resource file > menu.xml 만들기_

   ```xml
   // menu.xml
   <?xml version="1.0" encoding="utf-8" ?>
   <menu xmlns:android="http://schemas.android.com/apk/res/android">

        <item
            android:id="@+id/itemRed"
            android:title="배경색(빨강)"></item>

        <item
            android:id="@+id/itemGreen"
            android:title="배경색(초록)"></item>

        <item
            android:id="@+id/itemBlue"
            android:title="배경색(파랑)"></item>

        <item
            android:title="버튼 변경>> ">
            <menu>
                <item
                    android:id="@+id/subRotate"
                    android:title="버튼45도 회전"/>
                <item
                    android:id="@+id/subSize"
                    android:title="버튼 2배 확대" />
            </menu>
        </item>
    </menu>
   ```

2. Java 코딩 : onCreateOptionMenu() 메소드 오버라이딩(메뉴 파일 등록) -> 규칙이 정해져 있으므로 예시 코드 꼭 확인 -> **Code > Override Methods 클릭 > android.app.Activity에서 onCreateOptinoMenu() 찾기 > OK 클릭** -> return 지우기 -> 형식 그대로 유지 필요

   ```java
   // MainActivity.java
   package com.cookandroid.project7_1;

   import androidx.appcompat.app.AppCompatActivity;

   import android.os.Bundle;
   import android.view.Menu;
   import android.view.MenuInflater;
   import android.widget.Button;
   import android.widget.LinearLayout;

   public class MainActivity extends AppCompatActivity {

       LinearLayout baseLayout;
       Button button1;

       @Override
       public boolean onCreateOptionsMenu(Menu menu) {
           super.onCreateOptionsMenu(menu);
           MenuInflater mInflater = getMenuInflater();
           mInflater.inflate(R.menu.menu, menu);

           return true;
       }

       @Override
       protected void onCreate(Bundle savedInstanceState) {
           super.onCreate(savedInstanceState);
           setContentView(R.layout.activity_main);
           setTitle("배경색 바꾸기");

           baseLayout = (LinearLayout) findViewById(R.id.baseLayout);
           button1 = (Button) findViewById(R.id.button1);
       }
   }
   ```

3. Java 코딩 : onOptionsItemSelected() 메소드 오버라이딩(메뉴 선택 시 작동할 내용 코딩) -> **Code > Override Methods 클릭 > android.app.Activity에서 onOptionsItemSelected() 찾기 > OK 클릭** -> return 지우기 -> 코드 작성

   ```java
   package com.cookandroid.project7_1;

   import androidx.annotation.NonNull;
   import androidx.appcompat.app.AppCompatActivity;

   import android.graphics.Color;
   import android.os.Bundle;
   import android.view.Menu;
   import android.view.MenuInflater;
   import android.view.MenuItem;
   import android.widget.Button;
   import android.widget.LinearLayout;

   public class MainActivity extends AppCompatActivity {

       LinearLayout baseLayout;
       Button button1;

       @Override
       protected void onCreate(Bundle savedInstanceState) {
           super.onCreate(savedInstanceState);
           setContentView(R.layout.activity_main);
           setTitle("배경색 바꾸기");

           baseLayout = (LinearLayout) findViewById(R.id.baseLayout);
           button1 = (Button) findViewById(R.id.button1);
       }

       @Override
       public boolean onCreateOptionsMenu(Menu menu) {
           super.onCreateOptionsMenu(menu);
           MenuInflater mInflater = getMenuInflater();
           mInflater.inflate(R.menu.menu, menu);

           return true;
       }

       @Override
       public boolean onOptionsItemSelected(@NonNull MenuItem item) {
           switch(item.getItemId()) {
               case R.id.itemRed:
                   baseLayout.setBackgroundColor(Color.RED);
                   return true;
               case R.id.itemGreen:
                   baseLayout.setBackgroundColor(Color.GREEN);
                   return true;
               case R.id.itemBlue:
                   baseLayout.setBackgroundColor(Color.BLUE);
                   return true;
               case R.id.subRotate:
                   button1.setRotation(45);
                   return true;
               case R.id.subSize:
                   button1.setScaleX(2);
                   return true;
           }
       }
       return false;
   }
   ```

-> 결과

<img src="https://user-images.githubusercontent.com/96654391/169986018-00d579c8-ee6a-4a08-9be8-eae017c05e4b.png" width="300">

<img src="https://user-images.githubusercontent.com/96654391/169986027-341fe50a-e7e5-4f14-acc4-e54bb9631033.png" width="300">

<img src="https://user-images.githubusercontent.com/96654391/169986037-3906cc15-30b4-4ac4-bd3c-81d213b20c9c.png" width="300">

<img src="https://user-images.githubusercontent.com/96654391/169986044-14633668-358f-4647-b7ba-76d12ed636b4.png" width="300">

## 컨텍스트 메뉴

레이아웃 또는 버튼, 에디트텍스트 등의 위벳을 롱클릭 했을 때 화면 중앙에 나타나며 Windows의 팝업창과 유사함

-> 메뉴 설정 순서는 메뉴 설정과 유사

1. 메뉴 폴더 생성 및 위젯의 메뉴 XML 파일 생성 및 편집

2. Java 코딩 : onCreate 안에 registerForContextMenu() 로 등록

3. Java 코딩 : onCreateContextMenu() 메소드 오버라이딩

4. Java 코딩 : onContextItemSelected() 메소드 오버라이딩

## 토스트

화면에 잠깐 나타났다가 사라지는 메시지, 프로그래머가 디버깅 용도로 사용하기에도 적당함

`Toast.makeText(Context context, String message, int duration).show();`
-> duration: 화면에 나타나는 시간

<br>

<br>

자세한 코드는 실습을 직접하지는 않았으므로 12.2주차 ppt를 참고할 것
