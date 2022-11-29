---
title: "11.2주차"
excerpt: "11.2주차"
categories: [Android Studio]
tags: [Android Studio, Java]
toc: true
toc_sticky: true
---

📌 기말고사에는 AVD로 실행 결과 제출,,,,,,,,,,,,,,,

# 기타 위젯

## 프로그래스바, 시크바, 레이팅바

- 프로그래스바 : 작업의 진행 상황을 바나 원 형태로 제공
- 시크 바 : 프로그래스바와 대부분 비슷, 사용자 터치로 임의 조절 가능
- 레이팅바 : 진행 상황을 별 모양으로 표시

<br>
이 바는 자바와 연동이 되어야 의미가 있으나 기본적인 모양과 용도만 기억하자
<br>

-> 프로그래스바 xml

```xml
<ProgressBar
    style="?android:attr/progressBarStyleHorizontal"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:max="100"
    android:progress="20"
    android:secondaryProgress="50"/>
```

- style : 바 형태로 만들어줌
- max : 바의 최대값을 100으로
- progress : 처음 출력값
- secondaryProgress : progress 보다 연하게 살짝 나와있음
  <br>

-> 시크바 xml

```xml
<SeekBar
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:progress="20" />
```

-> 레이팅바 xml

```xml
<RatingBar
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:numStars="5"
    android:rating="1.5"
    android:stepSize="0.5" />
```

- rating : 초기값 별 개수 설정

<br>

<img src="https://user-images.githubusercontent.com/96654391/168758509-c7b263e5-8908-4601-99e3-b21e57138b78.png" width="300">

## 스크롤뷰

수직으로 스크롤하는 기능, 수평으로 스크롤하는 수평스크롤뷰가 따로있음 -> 주의할 점은 스크롤뷰에는 하나의 위젯만 넣을 수 있음

```xml
<?xml version="1.0" encoding="utf-8"?>
<ScrollView xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">

        <Button
            android:id="@+id/button1"
            android:layout_width="match_parent"
            android:layout_height="150dp"
            android:text="버튼1" />

        <Button
            android:id="@+id/button2"
            android:layout_width="match_parent"
            android:layout_height="150dp"
            android:text="버튼2" />

        <Button
            android:id="@+id/button3"
            android:layout_width="match_parent"
            android:layout_height="150dp"
            android:text="버튼3" />

        <Button
            android:id="@+id/button4"
            android:layout_width="match_parent"
            android:layout_height="150dp"
            android:text="버튼4" />

        <Button
            android:id="@+id/button5"
            android:layout_width="match_parent"
            android:layout_height="150dp"
            android:text="버튼5" />

        <Button
            android:id="@+id/button6"
            android:layout_width="match_parent"
            android:layout_height="150dp"
            android:text="버튼6" />

        <Button
            android:id="@+id/button7"
            android:layout_width="match_parent"
            android:layout_height="150dp"
            android:text="버튼7" />

    </LinearLayout>


</ScrollView>
```

<img src=https://user-images.githubusercontent.com/96654391/168759998-af2780a0-ea71-45fe-a965-67ad3de8ef7b.png" width="300">

## 슬라이딩드로어

슬라이딩드로어의 사전적 의미는 서랍으로, 위젯들을 서랍처럼 열어서 보여주거나 닫아서 감춤 -> 일반적인 형태를 잘 사용해야된다. handler에는 handle 명이 들어가며 버튼 id는 hanlder 명이 되어야 하고, content는 레이아웃 아이디가 되어야 한다.
<br>

->xml

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical" >

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="여기는 서랍 밖입니다." />

    <SlidingDrawer
        android:id="@+id/slidingdrawer"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:content="@+id/content"
        android:handle="@+id/handle"
        android:orientation="vertical" >

        <Button
            android:id="@+id/handle"
            android:layout_width="match_parent"
            android:layout_height="50dp"
            android:text="서랍 손잡이" />

        <LinearLayout
            android:id="@+id/content"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:background="#00FF00"
            android:gravity="center"
            android:orientation="vertical" >

            <TextView
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="여기는 서랍 안입니다."
                android:textColor="#000000"/>

        </LinearLayout>
    </SlidingDrawer>

</LinearLayout>
```

꼭 handle과 content를 맞춰야 작동함을 주의 해야된다. <br>

## 뷰플리퍼

안에 여러개의 위벳을 배치한 후, 필요에 따라서 화면을 왼쪽에서 오른쪽으로 밀어서 하나의 위젯씩 화면에 보여주는 방식의 뷰 컨테이너
<br>

<img src="https://user-images.githubusercontent.com/96654391/168791791-6e819b7e-9c99-4c60-bea0-ac833070e0c3.png" width="300"> <br>
<img src="https://user-images.githubusercontent.com/96654391/168791397-6efd9fad-c4a3-43fe-bfb0-2516b02c15e9.png" width="300">

->xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal">

        <Button
            android:id="@+id/btnPrev"
            android:layout_weight="1"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text=" 이전화면 " />

        <Button
            android:id="@+id/btnNext"
            android:layout_weight="1"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text=" 다음화면 " />
    </LinearLayout>

    <ViewFlipper
        android:id="@+id/viewFlipper1"
        android:layout_width="match_parent"
        android:layout_height="match_parent">
        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:background="#FF0000" ></LinearLayout>
        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:background="#00FF00" ></LinearLayout>
        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:background="#0000FF" ></LinearLayout>

        <ImageView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:src="@drawable/dog" />

    </ViewFlipper>

</LinearLayout>
```

<br>

->java

```java
package com.cookandroid.viewflipper;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.ViewFlipper;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Button btnPrev, btnNext;
        final ViewFlipper vFlipper;

        setTitle("2116313-손수경");
        btnPrev = (Button) findViewById(R.id.btnPrev);
        btnNext = (Button) findViewById(R.id.btnNext);
        vFlipper = (ViewFlipper) findViewById(R.id.viewFlipper1);

        btnPrev.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                vFlipper.showPrevious();
            }
        });

        btnNext.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                vFlipper.showNext();
            }
        });
    }
}
```

- ViewFlipper의 이벤트 기능에는 showNext()와 showPrev() 가 있다. <br>

<img src="https://user-images.githubusercontent.com/96654391/168768880-f4d47a0b-0ce9-429d-a01b-f8377fbb13a9.png" width="300">

<img src="https://user-images.githubusercontent.com/96654391/168768886-83cafd07-3b7a-4a79-a8f8-97ebd2363b1b.png" width="300">
 
<br>

버튼 클릭하면 옆화면 또는 뒷화면으로 넘어감
