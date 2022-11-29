---
title: "14.1주차"
excerpt: "14.1주차"
categories: [Android Studio]
tags: [Android Studio, Java]
toc: true
toc_sticky: true
---

# 파일 처리

## 내장 메모리 파일 처리

앱을 종료하고 다시 실행할 때 사용한 곳부터 이어서 작업하고 싶은 경우에 내장 메모리에 파일을 저장하고 읽어오는 방식을 활용 <br>
내장 메모리의 저장 위치 : `./data/data/패키지명/files 폴더([View] -> [Toll Windows] -> [Device File Explorer] 멘ㅍ에서 확인) <br>

<br>

- 파일을 읽기 위해 Context 클래스의 openFileInput() 메소드를 사용
- 파일을 쓰기 위해 Context 클래스의 openFileOutput() 메소드를 사용한다. 

### 내장 메모리 파일 처리 방법

1. openFileInput() / openFileOutput() 으로 파일 열기
2. read() / write()로 파일 읽기 / 쓰기
3. close() 로 파일 닫기

### 파일에 쓰기

1. 호출 결과를 Stream으로 받기 위한 코드, openFileOutput()는 예외가 있음. 예외처리 해야 됨. 
2. file.txt를 쓰기 모드로 연다. ***getBytes()*** 를 이용하여 문자열을 byte[] 형으로 변환. 파일 경로: `./data/data/패키지명/files/file.txt`
3. 쓰기 모드에는 MODE_PRIVATE나 MODE_APPEND를 사용할 수 있다. 
4. 파일 닫기

### 파일 읽기

1. openFileInput() 메소드를 사용해서 FileInputStream을 반환
2. byte[] 형의 변수 txt 선언
3. 입력 파일에서 읽어온 데이터를 txt에 저장
4. txt에 저장된 바이트 데이터를 문자열로 반환
5. 파일을 닫는다. 

## 파일 쓰기 코드 

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"

    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <Button
        android:id="@+id/btnWrite"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="내장 메모리에서 파일 쓰기" />

    <Button
        android:id="@+id/btnRead"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="내장 메모리에서 파일 읽기" />

</LinearLayout>
```
-> java
```java
package com.cookandroid.filehandling;

import androidx.appcompat.app.AppCompatActivity;

import android.content.Context;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.Toast;

import java.io.FileOutputStream;
import java.io.IOException;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        // 버튼에 대한 위젯 변수 선언
        Button btnWrite = (Button)findViewById(R.id.btnWrite);
        Button btnRead = (Button) findViewById(R.id.btnRead);

        btnWrite.setOnClickListener((new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                try {
                    FileOutputStream outFs = openFileOutput("file.txt", Context.MODE_PRIVATE);
                    String str = "쿡북 안드로이드";
                    outFs.write(str.getBytes());
                    outFs.close();
                    Toast.makeText(getApplicationContext(), "file.txt가 생성됨", Toast.LENGTH_SHORT).show();
                } catch(IOException e) {

                }
            }
        }));
    }
}
```

- 파일 쓰기 위해서는 반드시 예외 처리를 해주어야 할 것!

### 파일 읽기

```java
package com.cookandroid.filehandling;

import androidx.appcompat.app.AppCompatActivity;

import android.content.Context;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.Toast;

import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        // 버튼에 대한 위젯 변수 선언
        Button btnWrite = (Button)findViewById(R.id.btnWrite);
        Button btnRead = (Button) findViewById(R.id.btnRead);

        btnWrite.setOnClickListener((new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                try {
                    FileOutputStream outFs = openFileOutput("file.txt", Context.MODE_PRIVATE);
                    String str = "쿡북 안드로이드";
                    outFs.write(str.getBytes());
                    outFs.close();
                    Toast.makeText(getApplicationContext(), "file.txt가 생성됨", Toast.LENGTH_SHORT).show();
                } catch(IOException e) {

                }
            }
        }));
        btnRead.setOnClickListener((new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                try {
                    FileInputStream inFs = openFileInput("file.txt");
                    byte[] txt = new byte[30];
                    inFs.read(txt);
                    String str = new String(txt);
                    Toast.makeText(getApplicationContext(), str, Toast.LENGTH_SHORT);

                    inFs.close();
                } catch(IOException e) {
                    Toast.makeText(getApplicationContext(), "파일 없음", Toast.LENGTH_SHORT).show();
                }
            }
        }))
    }
}
```

너무 느려서 일단 여기까지만 올림 -> 추후 백업 필요 