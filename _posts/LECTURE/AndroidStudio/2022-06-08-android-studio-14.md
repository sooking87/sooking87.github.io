---
title: "chap05. 레이아웃 익히기"
excerpt: "chap05. 레이아웃 익히기"
categories: [Android Studio]
tags: [Android Studio, Java]
toc: true
toc_sticky: true
---

# 정리
![download1](https://user-images.githubusercontent.com/96654391/167545631-6c68f37f-b091-4a8b-b24e-1c94c047361e.png)
<br>

![download2](https://user-images.githubusercontent.com/96654391/167545866-09aa75fb-778c-4039-9092-e15ea27f039d.png)

# 연습 문제

## 4번 : 리니어레이아웃 사용

리니어 레이아웃만을 사용하여서 색상이 다른 레이아웃을 사용

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_weight="12"
        android:orientation="horizontal">


        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:orientation="vertical"
            android:layout_weight="2">

            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:layout_weight="3"
                android:background="#124512"></LinearLayout>

            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:layout_weight="3"
                android:background="#235623"></LinearLayout>
        </LinearLayout>

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:layout_weight="2"
            android:orientation="horizontal">

            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:layout_weight="2"
                android:background="#232323"/>

            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:layout_weight="2"
                android:background="#454545"/>

            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:layout_weight="2"
                android:background="#565656"/>
        </LinearLayout>

    </LinearLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_weight="12"
        android:background="#0000ff"></LinearLayout>

</LinearLayout>
```

<img width="322" alt="화면 캡처 2022-05-10 141221" src="https://user-images.githubusercontent.com/96654391/172637808-7facb715-8094-46b7-9837-a12648636444.png">

## +a: gravity 속성

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
        android:orientation="horizontal">

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="전화번호"
            android:textSize="20dp"/>

        <EditText
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:hint="000-0000-0000"
            android:textSize="20dp"/>
    </LinearLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:gravity="right">

        <EditText
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"/>

        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="입력"
            android:textSize="20dp" />

        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="취소"
            android:textSize="20dp" />
    </LinearLayout>
</LinearLayout>
```


<img width="322" alt="화면 캡처 2022-05-10 141221" src="https://user-images.githubusercontent.com/96654391/172639514-951a4922-d375-4842-86d3-b6c771bb8af1.png"> <br>

위에 editText 칸이 빈칸임에도 불구하고 gravity를 오른쪽으로 하였으므로 다음과 같이 나타날 수 있다.(2번째줄)

## 5번: Relative Layout

![download3](https://user-images.githubusercontent.com/96654391/167546793-d0a40ade-29ee-432b-a979-b9bab8eeaa4b.png) <br>

-> 하나의 기준 버튼을 기준으로 다른 컴포넌트들을 배치 <br>


![download3](https://user-images.githubusercontent.com/96654391/167547432-19a4f60b-d7ba-4682-aa62-49657bba8a1d.png)

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:layout_margin="10dp">

    <!--layout_centerHorizontal, layout_centerVertical: 정 중앙 배치-->
    <Button
        android:id="@+id/baseBtn"
        android:layout_width="150dp"
        android:layout_height="150dp"
        android:text="기준 위젯"
        android:textSize="20dp"
        android:layout_centerHorizontal="true"
        android:layout_centerVertical="true" />

    <!--layout_alignTop, layout_toLeftOf-->
    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignTop="@+id/baseBtn"
        android:layout_toLeftOf="@+id/baseBtn"
        android:text="1번" />

    <!--layout_above, layout_alignLeft-->
    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_above="@+id/baseBtn"
        android:layout_alignLeft="@+id/baseBtn"
        android:text="2번" />

    <!--layout_toRightOf, layout_alignBottom-->
    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_toRightOf="@+id/baseBtn"
        android:layout_alignBottom="@+id/baseBtn"
        android:text="3번" />

    <!--layout_below, layout_alignRight-->
    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@+id/baseBtn"
        android:layout_alignRight="@+id/baseBtn"
        android:text="3번" />

    <!--layout_alignParentBottom, layout_centerVertical-->
    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentBottom="true"
        android:layout_centerVertical="true"
        android:text="좌측" />
</RelativeLayout>
```

<img width="312" alt="화면 캡처 2022-05-10 141221" src="https://user-images.githubusercontent.com/96654391/172748095-92c158e2-f6f7-4213-b521-093c7546e912.png">

## TableLayout 계산기 만들기

-> xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<TableLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:layout_margin="10dp">

    <TableRow>
        <EditText
            android:id="@+id/Edit1"
            android:layout_span="5"
            android:layout_weight="5"
            android:hint="숫자 1 입력" />
    </TableRow>
    <TableRow>
        <EditText
            android:id="@+id/Edit2"
            android:layout_span="5"
            android:layout_weight="5"
            android:hint="숫자 2 입력" />
    </TableRow>
    <TableRow>
        <Button
            android:id="@+id/BtnNum0"
            android:layout_weight="1"
            android:text="0" />
        <Button
            android:id="@+id/BtnNum1"
            android:layout_weight="1"
            android:text="1" />
        <Button
            android:id="@+id/BtnNum2"
            android:layout_weight="1"
            android:text="2" />
        <Button
            android:id="@+id/BtnNum3"
            android:layout_weight="1"
            android:text="3" />
        <Button
            android:id="@+id/BtnNum4"
            android:layout_weight="1"
            android:text="4" />
    </TableRow>
    <TableRow>
        <Button
            android:id="@+id/BtnNum5"
            android:layout_weight="1"
            android:text="5" />
        <Button
            android:id="@+id/BtnNum6"
            android:layout_weight="1"
            android:text="6" />
        <Button
            android:id="@+id/BtnNum7"
            android:layout_weight="1"
            android:text="7" />
        <Button
            android:id="@+id/BtnNum8"
            android:layout_weight="1"
            android:text="8" />
        <Button
            android:id="@+id/BtnNum9"
            android:layout_weight="1"
            android:text="9" />
    </TableRow>
    <TableRow>
        <Button
            android:id="@+id/BtnAdd"
            android:layout_marginTop="20dp"
            android:layout_span="5"
            android:layout_weight="5"
            android:text="더하기"/>
    </TableRow>

    <TableRow>
        <Button
            android:id="@+id/BtnSub"
            android:layout_marginTop="20dp"
            android:layout_span="5"
            android:layout_weight="5"
            android:text="빼기"/>
    </TableRow>

    <TableRow>
        <Button
            android:id="@+id/BtnMul"
            android:layout_marginTop="20dp"
            android:layout_span="5"
            android:layout_weight="5"
            android:text="곱하기"/>
    </TableRow>

    <TableRow>
        <Button
            android:id="@+id/BtnDiv"
            android:layout_marginTop="20dp"
            android:layout_span="5"
            android:layout_weight="5"
            android:text="나누기"/>
    </TableRow>
    <TableRow>
        <TextView
            android:id="@+id/TextResult"
            android:layout_marginTop="20dp"
            android:layout_weight="5"
            android:text="계산 결과: "
            android:textColor="#ff0000"
            android:textSize="20dp"/>
    </TableRow>


</TableLayout>
```
<br>

-> java
```java
package com.cookandroid.chap04_4;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextClock;
import android.widget.TextView;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

    EditText edit1, edit2;
    Button btnAdd, btnSub, btnMul, btnDiv;
    TextView textResult;
    String num1, num2;
    Integer result;
    Button[] numButtons = new Button[10];
    Integer[] numBtnIds = {R.id.BtnNum0, R.id.BtnNum1, R.id.BtnNum2, R.id.BtnNum3,
            R.id.BtnNum4,R.id.BtnNum5, R.id.BtnNum6, R.id.BtnNum7, R.id.BtnNum8, R.id.BtnNum9};
    int i;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        setTitle("계산기");

        edit1 = (EditText) findViewById(R.id.Edit1);
        edit2 = (EditText) findViewById(R.id.Edit2);
        btnAdd = (Button) findViewById(R.id.BtnAdd);
        btnSub = (Button) findViewById(R.id.BtnSub);
        btnMul = (Button) findViewById(R.id.BtnMul);
        btnDiv = (Button) findViewById(R.id.BtnDiv);
        for (i = 0; i < numButtons.length; i++) {
            numButtons[i] = (Button) findViewById(numBtnIds[i]);
        }
        textResult = (TextView) findViewById(R.id.TextResult);

        btnAdd.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                num1 = edit1.getText().toString();
                num2 = edit2.getText().toString();
                result = Integer.parseInt(num1) + Integer.parseInt(num2);
                textResult.setText("계산 결과: " + result.toString());
            }
        });

        btnSub.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                num1 = edit1.getText().toString();
                num2 = edit2.getText().toString();
                result = Integer.parseInt(num1) - Integer.parseInt(num2);
                textResult.setText("계산 결과: " + result.toString());
            }
        });

        btnMul.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                num1 = edit1.getText().toString();
                num2 = edit2.getText().toString();
                result = Integer.parseInt(num1) * Integer.parseInt(num2);
                textResult.setText("계산 결과: " + result.toString());
            }
        });

        btnDiv.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                num1 = edit1.getText().toString();
                num2 = edit2.getText().toString();
                result = Integer.parseInt(num1) / Integer.parseInt(num2);
                textResult.setText("계산 결과: " + result.toString());
            }
        });

        // 숫자 버튼 리스너
        for (i = 0; i < numBtnIds.length; i++) {
            final int index; // 꼭 필dy하다고 함
            index = i;

            numButtons[index].setOnClickListener(new View.OnClickListener() {
                @Override
                public void onClick(View view) {
                    if (edit1.isFocused()) {
                        num1 = edit1.getText().toString() + numButtons[index].getText().toString();
                        edit1.setText(num1);
                    }
                    else if (edit2.isFocused()){
                        num2 = edit2.getText().toString() + numButtons[index].getText().toString();
                        edit2.setText(num2);
                    } else {
                        Toast.makeText(getApplicationContext(), "먼저 에디트텍스트를 선택하세요", Toast.LENGTH_SHORT).show();
                    }
                }
            });
        }

    }
}
```