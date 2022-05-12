---
title: "11.1주차"
excerpt: "11.1주차"
categories: [Android Studio]
tags: [Android Studio, Java]
toc: true
toc_sticky: true
---

# 고급 위젯 다루기

## 아날로그 시계, 디지털 시계

## 크로노미터

타이머 형식 위젯으로 **시간을 측정** 할 때 사용

- start(), stop(), reset() 메소드
- format 속성 : 시간 측정을 시, 분, 초 형식으로 출력 <br>

-> xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <AnalogClock
        android:layout_margin="10dp"
        android:layout_width="match_parent"
        android:layout_height="wrap_content" />

    <DigitalClock
        android:layout_margin="10dp"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:gravity="center"/>

    <Chronometer
        android:layout_margin="10dp"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:format="예약 시간 %s"
        android:gravity="center"
        android:textSize="20dp"/>

</LinearLayout>
```

- Chronometer의 format 속성 : 시간을 보여줌 <br>

<img src="https://user-images.githubusercontent.com/96654391/168019376-155fb045-2b3d-41ae-9c57-ea04604cd6a6.png" width=200>

## 타임 피커, 데이트피커, 캘린더뷰

- 타임 피커 : 시간을 표시, 조절
- 데이트 피커 && 캘린더뷰 : 날짜를 표시하고 조절하는 기능
  <br> <br>

-> xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <TimePicker
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:timePickerMode="spinner" />

    <DatePicker
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:datePickerMode="spinner" />

    <CalendarView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:showWeekNumber="false" />

</LinearLayout>
```

<img src="https://user-images.githubusercontent.com/96654391/168019382-d891281b-612f-41ba-98e2-de380e570490.png" width=200>

## 실습

-> xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:layout_margin="10dp">


    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="vertical">

        <Chronometer
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:format="예약에 걸린 시간 %s"
            android:gravity="center"
            android:textSize="20dp" />

        <Button
            android:id="@+id/btnStart"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="예약 시작"
            android:textSize="20dp" />


    </LinearLayout>

    <RadioGroup
        android:layout_width="wrap_content"
        android:layout_height="wrap_content" >

        <RadioButton

            android:id="@+id/rdoCal"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:checked="true"
            android:text="날짜 설정(캘린더뷰)" />

        <RadioButton
            android:id="@+id/rdoTime"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"

            android:text="시간 설정" />

    </RadioGroup>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1"
        android:orientation="vertical">

        <FrameLayout
            android:layout_gravity="center"
            android:layout_width="match_parent"
            android:layout_height="match_parent">

            <CalendarView
                android:id="@+id/calenderView1"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:showWeekNumber="false" />

            <TimePicker
                android:id="@+id/timePicker1"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:timePickerMode="spinner" />

        </FrameLayout>

    </LinearLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:layout_margin="10dp">

        <Button
            android:id="@+id/btnEnd"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="예약 완료" />

        <TextView
            android:id="@+id/tvYear"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="0000" />

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="년" />

        <TextView
            android:id="@+id/tvMonth"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="00" />

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="월" />

        <TextView
            android:id="@+id/tvDay"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="00" />

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="일" />

        <TextView
            android:id="@+id/tvHour"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="00" />

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="시" />


        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="분 예약됨" />


    </LinearLayout>
</LinearLayout>
```

- FrameLayout
- 밑에 있는 10개 TextView : 년월일시분을 표시하기 위한 컴포넌트
- 나중에 그림이랑 맞춰서 잘보길,,,,
  <br>
  -> java

```java
package com.cookandroid.project6_1;

import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;

import android.graphics.Color;
import android.os.Bundle;
import android.os.SystemClock;
import android.view.View;
import android.widget.Button;
import android.widget.CalendarView;
import android.widget.Chronometer;
import android.widget.RadioButton;
import android.widget.TextView;
import android.widget.TimePicker;

public class MainActivity extends AppCompatActivity {

    // 위젯 변수 설정
    Chronometer chrono;
    Button btnStart, btnEnd;
    RadioButton rdoCal, rdoTime;
    CalendarView calView;
    TimePicker tPicker;
    TextView tvYear, tvMonth, tvDay, tvHour, tvMinute;
    int selectYear, selectMonth, selectDay;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        setTitle("시간 예약");

        // 위젯 변수 12개에 위젯 대입
        chrono = (Chronometer) findViewById(R.id.chronometer1);
        btnStart = (Button)findViewById(R.id.btnStart);
        btnEnd = (Button) findViewById(R.id.btnEnd);

        // 라디오버튼 2개
        rdoCal = (RadioButton) findViewById(R.id.rdoCal);
        rdoTime = (RadioButton) findViewById(R.id.rdoTime);

        // FrameLayout의 2개 위젯
        tPicker = (TimePicker) findViewById(R.id.timePicker1);
        calView = (CalendarView) findViewById(R.id.calenderView1);

        // 텍스트뷰 중에서 연, 워르 일, 시, 분 숫자
        tvYear = (TextView) findViewById(R.id.tvYear);
        tvMonth = (TextView) findViewById(R.id.tvMonth);
        tvDay = (TextView) findViewById(R.id.tvDay);
        tvHour = (TextView) findViewById(R.id.tvHour);
        tvMinute = (TextView) findViewById(R.id.tvMinute);

        tPicker.setVisibility(View.INVISIBLE);
        calView.setVisibility(View.INVISIBLE);

        rdoCal.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                tPicker.setVisibility(View.INVISIBLE);
                calView.setVisibility(View.VISIBLE);
            }
        });

        rdoTime.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                tPicker.setVisibility(View.VISIBLE);
                calView.setVisibility(View.INVISIBLE);
            }
        });

        // 타이머 설정
        btnStart.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                // chronometer이 작동하게 해야됨
                chrono.setBase(SystemClock.elapsedRealtime()); // 타이머 클리어 상태
                chrono.start();
                chrono.setTextColor(Color.RED);
            }
        });

        // 예약 완료 버튼 클릭시 날짜, 시간을 가져온다.
        btnEnd.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                chrono.stop();
                chrono.setTextColor(Color.BLUE);
                tvYear.setText(Integer.toString(selectYear));
                tvMonth.setText(Integer.toString(selectMonth));
                tvDay.setText(Integer.toString(selectDay));

                // 시간 분은 타임피크에서 가져옴
                tvHour.setText(Integer.toString(tPicker.getCurrentHour()));
                tvMinute.setText(Integer.toString(tPicker.getCurrentMinute()));

            }
        });

        calView.setOnDateChangeListener(new CalendarView.OnDateChangeListener() {
            @Override
            public void onSelectedDayChange(@NonNull CalendarView calendarView, int year, int month, int day) {
                selectYear = year;
                selectMonth = month + 1;
                selectDay = day;
            }
        });

    }
}
```

예약 시작(btnStart)을 누르면 chrono가 start되면서 시간 count <br>

예약 완료(btnEnd)를 누르면 chrono가 stop되고, selectYear, selectMonth, selectDay 변수에 값을 넣어준다. -> 이때 이벤트 리스너가 **_setOnDateChangeListener(new CalendarView.OnDateChangeListener())_** 라는 점!!! 주의 <br>

그리고 setText를 통해서 글씨를 써주는데, tvHour와 tvMinute는 tPicker을 통해서 가져올 수 있다.
<br>

결과 <br>

<img src="https://user-images.githubusercontent.com/96654391/168029720-0911cd3a-e4eb-4f8b-a899-da5c3b3d96f1.png" width=200>
