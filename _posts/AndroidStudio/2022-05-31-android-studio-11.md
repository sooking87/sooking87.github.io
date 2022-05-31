---
title: "13.2주차"
excerpt: "13.2주차"
categories: [Android Studio]
tags: [Android Studio, Java]
toc: true
toc_sticky: true
---

📌 저번 주에 했던 실습을 해설하는 강의

## activity_main.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"

    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:gravity="center_horizontal"
    android:orientation="vertical">

    <TextView
        android:id="@+id/tvName"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="사용자 이름" />

    <TextView
        android:id="@+id/tvEmail"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="이메일" />

    <Button
        android:id="@+id/button1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="여기를 클릭" />

</LinearLayout>
```

## dialog1.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="사용자 이름" />

    <EditText
        android:id="@+id/dlgEdt1"
        android:layout_width="match_parent"
        android:layout_height="wrap_content" />

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="이메일" />

    <EditText
        android:id="@+id/dlgEdt2"
        android:layout_width="match_parent"
        android:layout_height="wrap_content" />
</LinearLayout>
```

## toast1.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#ff0000"
    android:gravity="center">

    <ImageView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:src="@drawable/btn_star_big_on" />

    <TextView
        android:id="@+id/toastText1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="TextView"
        android:textSize="20dp" />

    <ImageView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:src="@drawable/btn_star_big_on" />

</LinearLayout>
```

## MainActivity.java

```java
package com.cookandroid.project7_3;

import androidx.appcompat.app.AlertDialog;
import androidx.appcompat.app.AppCompatActivity;

import android.content.DialogInterface;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {
    TextView tvName, tvEmail;
    Button button1;
    EditText dlgEdtName, dlgEdtEmail;
    TextView toastText;
    View dialogView, toastView; // dialog1.xml, toast1.cml 저장

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        setTitle("사용자 정보 입력");

        tvName = (TextView) findViewById(R.id.tvName);
        tvEmail = (TextView) findViewById(R.id.tvEmail);
        button1 = (Button) findViewById(R.id.button1);

        button1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                dialogView = (View) View.inflate(MainActivity.this, R.layout.dialog1, null);
                AlertDialog.Builder dlg = new AlertDialog.Builder(MainActivity.this);

                dlg.setTitle("사용자 정보 입력"); // 대화 상자의 제목
                dlg.setIcon(R.drawable.ic_menu_allfriends); // 제목 옆에 아이콘
                dlg.setView(dialogView);
                dlg.setPositiveButton("확인", new DialogInterface.OnClickListener() {
                    @Override
                    public void onClick(DialogInterface dialogInterface, int i) {
                        dlgEdtName = (EditText) dialogView.findViewById(R.id.dlgEdt1);
                        dlgEdtEmail = (EditText) dialogView.findViewById(R.id.dlgEdt2);

                        tvName.setText(dlgEdtName.getText().toString());
                        tvEmail.setText(dlgEdtEmail.getText().toString());
                    }
                });
                dlg.setNegativeButton("취소", new DialogInterface.OnClickListener() {
                    @Override
                    public void onClick(DialogInterface dialog, int i) {
                        Toast toast = new Toast(MainActivity.this);
                        toastView = (View) View.inflate(MainActivity.this, R.layout.toast1, null);
                        toastText = (TextView) toastView.findViewById(R.id.toastText1);
                        toastText.setText("취소했습니다.");
                        toast.setView(toastView);
                        toast.show();
                    }
                });
                dlg.show();
            }
        });
    }
}
```

자바 코드에서 따로 만든 xml 가져오는 방법

```java
public class MainActivity extends AppCompatActivity {
    ...
    View dialogView, toastView; // dialog1.xml, toast1.cml 저장

     @Override
    protected void onCreate(Bundle savedInstanceState) {
        dialogView = (View) View.inflate(MainActivity.this, R.layout.dialog1, null);
        ...

        dlg.setNegativeButton("취소", new DialogInterface.OnClickListener() {
            @Override
            public void onClick(DialogInterface dialog, int i) {
                Toast toast = new Toast(MainActivity.this);
                toastView = (View) View.inflate(MainActivity.this, R.layout.toast1, null);
                ...
            }
        )}
    }
```

## 결과

![download1](https://user-images.githubusercontent.com/96654391/171127368-33a881b4-1bcd-4928-a9df-250b23db7f6c.png)
![download2](https://user-images.githubusercontent.com/96654391/171127377-ddefd5f9-4acb-409d-b2ff-d4af28fd5ae5.png)
![download3](https://user-images.githubusercontent.com/96654391/171127384-ddf19e8d-b5f6-49d0-a4f6-d91ce100259a.png) <br>

toast 창에서 취소버튼 클릭 <br>

![화면 캡처 2022-05-31 171527](https://user-images.githubusercontent.com/96654391/171127391-8508f59b-3cf8-4fcc-b121-f17f133e7978.png)
