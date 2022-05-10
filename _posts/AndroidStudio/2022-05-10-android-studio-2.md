---
title: "Linear 레이아웃 / Relative 레이아웃"
excerpt: "Linear 레이아웃 / Relative 레이아웃"
categories: [Android Studio]
tags: [Android Studio, Java]
toc: true
toc_sticky: true
---

- 레이아웃 기본 개념
- Linear 레이아웃
- Relative 레이아웃

![download1](https://user-images.githubusercontent.com/96654391/167545631-6c68f37f-b091-4a8b-b24e-1c94c047361e.png)
<br>

![download2](https://user-images.githubusercontent.com/96654391/167545866-09aa75fb-778c-4039-9092-e15ea27f039d.png)

## 레이아웃의 대표적인 속성

![download1](https://user-images.githubusercontent.com/96654391/167546249-034572a5-47f7-4e71-8cd3-0172a657c297.png)

<br>

![download2](https://user-images.githubusercontent.com/96654391/167546251-6270ddd0-cf5e-4b75-b0c2-727ebf69d5b6.png)

<br>

![download3](https://user-images.githubusercontent.com/96654391/167546256-0200696d-bd03-4c9c-9ec2-ebbd976d0122.png)

<br>

![download2](https://user-images.githubusercontent.com/96654391/167546717-f49c3880-6adb-4d86-8e62-e384a4484b86.png)
<br>

-> layout_weight 예시

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_weight="1"
        android:orientation="vertical"
        android:gravity="center">

        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="버튼1"
            android:textSize="20dp"
            android:layout_marginBottom="10dp"/>

        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="버튼2"
            android:textSize="20dp" />

    </LinearLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_weight="1"
        android:orientation="horizontal"
        android:gravity="center"
        android:background="#00ff00">

        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="버튼3"
            android:textSize="20dp"
            android:background="#00ff00"
            android:layout_marginRight="10dp"/>

        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="버튼4"
            android:textSize="20dp"
            android:background="#00ff00"/>

    </LinearLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_weight="1"
        android:orientation="vertical"
        android:gravity="center"
        android:background="#0000ff">

        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="버튼5"
            android:textSize="20dp"
            android:background="#0000ff"
            android:layout_marginBottom="10dp"/>

        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="버튼6"
            android:textSize="20dp"
            android:background="#0000ff"/>

    </LinearLayout>

</LinearLayout>
```

<img width="185" alt="download2" src="https://user-images.githubusercontent.com/96654391/167547122-4c5a65c2-a49e-4d25-acbf-747d819802c0.png">

## Linear Layout

## 중복 Linear Layout

-> .xml 코드

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:layout_margin="20dp"
    android:orientation="vertical">

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginBottom="10dp">

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="전화번호"
            android:textSize="25dp"/>

        <EditText
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:hint="000-0000-0000"
            android:textSize="25dp"/>

    </LinearLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:gravity="right">

        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="입력"
            android:background="#5500ff00"
            android:textSize="20dp"
            android:layout_marginRight="10dp"/>

        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="취소"
            android:background="#5500ff00"
            android:textSize="20dp" />

    </LinearLayout>

</LinearLayout>
```

<img src="https://user-images.githubusercontent.com/96654391/167546465-57a4d4fa-5a06-4cbb-8ca8-457eb741130e.png" width="185">

## Relative Layout

### 기본(아직까진 상대적 위치 조정 X)

![download3](https://user-images.githubusercontent.com/96654391/167546793-d0a40ade-29ee-432b-a979-b9bab8eeaa4b.png)

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <Button
        android:id="@+id/button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentTop="true"
        android:layout_centerHorizontal="true"
        android:text="위쪽"
        android:textSize="20dp"/>

    <Button
        android:id="@+id/button3"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentLeft="true"
        android:layout_centerVertical="true"
        android:text="좌측"
        android:textSize="20dp"/>

    <Button
        android:id="@+id/button4"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentRight="true"
        android:layout_centerVertical="true"
        android:text="우측"
        android:textSize="20dp"/>

    <Button
        android:id="@+id/button5"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerInParent="true"
        android:text="중앙"
        android:textSize="20dp"/>

    <Button
        android:id="@+id/button6"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentBottom="true"
        android:layout_centerHorizontal="true"
        android:text="아래"
        android:textSize="20dp"/>
</RelativeLayout>
```

<img src="https://user-images.githubusercontent.com/96654391/167547307-640c5b6d-99f6-4cca-9012-044eba9602d6.png" width="185">

### 상대적 레이아웃

-> 하나의 기준 버튼을 기준으로 다른 컴포넌트들을 배치

![download3](https://user-images.githubusercontent.com/96654391/167547432-19a4f60b-d7ba-4682-aa62-49657bba8a1d.png)

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <Button
        android:id="@+id/baseBtn"
        android:layout_width="150dp"
        android:layout_height="150dp"
        android:layout_centerHorizontal="true"
        android:layout_centerVertical="true"
        android:text="기준위젯"
        android:textSize="20dp"/>

    <Button
        android:id="@+id/button2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignTop="@+id/baseBtn"
        android:layout_toLeftOf="@+id/baseBtn"
        android:text="1번"
        android:textSize="20dp"/>

    <Button
        android:id="@+id/button3"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignBaseline="@+id/baseBtn"
        android:layout_toLeftOf="@+id/baseBtn"
        android:text="2번"
        android:textSize="20dp"/>

    <Button
        android:id="@+id/button4"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignBottom="@+id/baseBtn"
        android:layout_toLeftOf="@+id/baseBtn"
        android:text="3번"
        android:textSize="20dp" />

    <Button
        android:id="@+id/button5"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignLeft="@+id/baseBtn"
        android:layout_above="@+id/baseBtn"
        android:text="4번"
        android:textSize="20dp"/>

    <Button
        android:id="@+id/button6"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignRight="@+id/baseBtn"
        android:layout_below="@id/baseBtn"
        android:text="5번"
        android:textSize="20dp"/>

    <Button
        android:id="@+id/button7"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_toRightOf="@+id/baseBtn"
        android:layout_above="@+id/baseBtn"
        android:text="6번"
        android:textSize="20dp" />

</RelativeLayout>
```

<img src="https://user-images.githubusercontent.com/96654391/167547519-6f356ef6-2aad-49a2-954b-f52e8584e2e2.png" width=185>
