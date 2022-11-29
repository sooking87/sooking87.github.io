---
title: "10.2주차"
excerpt: "10.2주차"
categories: [Android Studio]
tags: [Android Studio, Java]
toc: true
toc_sticky: true
---

📌 과제2 제출을 위한 코드 작성을 함

## 과제 2-1

-> xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <CheckBox
        android:id="@+id/enabled"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Enabled 속성" />

    <CheckBox
        android:id="@+id/clickable"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Clickable 속성" />

    <CheckBox
        android:id="@+id/rotate"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="30도 회전" />

    <Button
        android:id="@+id/btn"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="100dp"
        android:clickable="false"
        android:enabled="false"
        android:text="BUTTON" />

</LinearLayout>
```

- enabled 속성 : 버튼 구동의 여부 결정
- clickable 속성 : 버튼이 enabled 되었더라도 클릭의 여부 결정
  <br>

-> java

```java
package com.cookandroid.sohnsookyoung_r21;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.CheckBox;
import android.widget.CompoundButton;

public class MainActivity extends AppCompatActivity {

    CheckBox enabled, clickable, rotate;
    Button btn;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        setTitle("손수경-2116313");

        enabled = (CheckBox) findViewById(R.id.enabled);
        clickable = (CheckBox) findViewById(R.id.clickable);
        rotate = (CheckBox) findViewById(R.id.rotate);
        btn = (Button) findViewById(R.id.btn);

        enabled.setOnCheckedChangeListener(new CompoundButton.OnCheckedChangeListener() {
            @Override
            public void onCheckedChanged(CompoundButton compoundButton, boolean b) {
                if (enabled.isChecked()) {
                    btn.setEnabled(true);
                } else {
                    btn.setEnabled(false);
                }
            }
        });

        clickable.setOnCheckedChangeListener(new CompoundButton.OnCheckedChangeListener() {
            @Override
            public void onCheckedChanged(CompoundButton compoundButton, boolean b) {
                if (clickable.isClickable()) {
                    btn.setClickable(true);
                } else {
                    btn.setClickable(false);
                }
            }
        });

        rotate.setOnCheckedChangeListener(new CompoundButton.OnCheckedChangeListener() {
            @Override
            public void onCheckedChanged(CompoundButton compoundButton, boolean b) {
                if (rotate.isChecked()) {
                    btn.setRotation(30);
                } else {
                    btn.setRotation(0);
                }
            }
        });
    }
}
```

- 체크 박스 리스너 : setOnCheckedChangeListener(new C..)
- 체크가 되었다면 : 컴포넌트.isChecked()
- setEnabled()
- setClickable
- setRotation(deg) : deg 만큼 회전

### 결과

<img src="https://user-images.githubusercontent.com/96654391/167614736-90a68973-9c31-4adc-8e36-fb6c3eca05b2.png" width="250"> <br>
<img src="https://user-images.githubusercontent.com/96654391/167614751-50212bdc-6620-4e52-afa2-899052eed350.png" width="250"> <br>
<img src="https://user-images.githubusercontent.com/96654391/167614756-18729e8b-0b77-44bb-86d6-2c68ea594b74.png" width="250">
<br>

간단한 예제지만 처음에 id 불러오는 과정에서 3개의 checkBox 아이디를 모두 enabled로 잡아놔서 오류가 났었음! 주의!!

## 과제 2-2

-> xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:layout_margin="30dp">


    <Button
        android:id="@+id/btn"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="회전하기"
        android:layout_gravity="center"
        android:drawableLeft="@drawable/ic_launcher_foreground"
        android:drawableRight="@drawable/ic_launcher_foreground"/>


    <ImageView
        android:id="@+id/img"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center"
        android:src="@drawable/dog" />


</LinearLayout>
```

- 버튼에 안드로이드 이미지 넣기(기존에 있던 이미지를 활용하면 된다!)
- `android:background="@drawable/ic_launcher_foreground"` : 버튼 배경에 사진이 들어감
- `android:drawableLeft="@drawable/ic_launcher_foreground"` : 버튼 왼쪽에 사진이 들어감
- `android:drawableRight="@drawable/ic_launcher_foreground"` : 버튼 오른쪽에 사진이 들어감

<br>

-> java

```java
package com.cookandroid.sohnsookyoung_r22;

import androidx.appcompat.app.AppCompatActivity;

import android.media.Image;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.ImageView;

public class MainActivity extends AppCompatActivity {

    Button btn;
    ImageView img;
    float angle = 0;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        setTitle("손수경-2116313");

        btn = (Button) findViewById(R.id.btn);
        img = (ImageView) findViewById(R.id.img);

        btn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                angle += 10;
                img.setRotation(angle);
            }
        });

    }
}
```

### 결과

<img src="https://user-images.githubusercontent.com/96654391/167615592-759a28dc-0ab5-4d68-b455-47f5736ce832.png" width="250">
