---
title: "13.1주차"
excerpt: "13.1주차"
categories: [Android Studio]
tags: [Android Studio, Java]
toc: true
toc_sticky: true
---

# 대화 상자

## 대화 상자

화면에 메시지를 알려준 후 확인이나 취소 같은 사용자의 선택을 받아들일 때 사용.

![download1](https://user-images.githubusercontent.com/96654391/170441069-b67b4e37-bf9b-42ec-976f-4ad8007ca3c0.png) <br>

### 기본 대화상자 예제

-> xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"

    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:gravity="center_horizontal"
    android:orientation="vertical">

    <Button
        android:id="@+id/button1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="대화 상자" />



</LinearLayout>
```

-> java

```java
package com.cookandroid.exam7_14_16;

import androidx.appcompat.app.AlertDialog;
import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        final Button button1 = (Button) findViewById(R.id.button1);
        button1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                AlertDialog.Builder dlg = new AlertDialog.Builder(MainActivity.this);
                 // 액티비티명.this
                dlg.setTitle("제목입니다.");
                dlg.setMessage("이곳이 내용입니다.");
                dlg.setIcon(R.mipmap.ic_launcher);
                dlg.setPositiveButton("확인", null); // 확인버튼
                dlg.show();
            }
        });
    }
}
```

<br>

결과 <br>

<img src="https://user-images.githubusercontent.com/96654391/170443497-63d12cd8-9386-4b5f-a1d3-fb34e6d620d6.png" width="300">

<br>

null을 넣었으므로 확인을 눌러도 아무런 반응이 없이 그냥 창이 닫힌다.

<br>
확인 버튼을 눌렀을 때, 확인을 눌렀네요 를 Toast.makeText()로 띄운다. <br>

->xml : 위와 동일 <br>

-> java

```java
package com.cookandroid.exam7_14_16;

import androidx.appcompat.app.AlertDialog;
import androidx.appcompat.app.AppCompatActivity;

import android.content.DialogInterface;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        final Button button1 = (Button) findViewById(R.id.button1);
        button1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                AlertDialog.Builder dlg = new AlertDialog.Builder(MainActivity.this);
                 // 액티비티명.this
                dlg.setTitle("제목입니다.");
                dlg.setMessage("이곳이 내용입니다.");
                dlg.setIcon(R.mipmap.ic_launcher);
                dlg.setPositiveButton("확인", new DialogInterface.OnClickListener() {
                    @Override
                    public void onClick(DialogInterface dialogInterface, int i) {
                        Toast.makeText(MainActivity.this, "확인을 눌렀네요", Toast.LENGTH_SHORT).show();
                    }
                });
                dlg.show();
            }
        });
    }
}
```

결과 <br>

대화 상자 출력창은 위와 동일 위 대화 상자에서 확인을 눌렀을 때, 다음과 같이 나옴 <br>

<img src="https://user-images.githubusercontent.com/96654391/170444314-ec66554a-822e-4e52-8e14-faa1778e9b3f.png" width="300">

### 목록 대화 상자 예제

목록 대화 상자 -> 대화 상자에 리스트 형태의 목록을 출력하고 그 중 하나를 선택할 때 사용, 비슷한 형태로 매번 사용하므로 **_코드를 통째로 기억함이 좋다_**

<br>

-> java

```java
package com.cookandroid.exam7_14_16;

import androidx.appcompat.app.AlertDialog;
import androidx.appcompat.app.AppCompatActivity;

import android.content.DialogInterface;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        final Button button1 = (Button) findViewById(R.id.button1);
        final String[] versionArray = new String[] {"파이", "Q(10)", "R(11)"};
        button1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                AlertDialog.Builder dlg = new AlertDialog.Builder(MainActivity.this);
                 // 액티비티명.this
                dlg.setTitle("좋아하는 버전은?");
                // dlg.setMessage("이곳이 내용입니다."); 지워 줘야지 배열이 나옴
                dlg.setIcon(R.mipmap.ic_launcher);
                dlg.setItems(versionArray,
                        new DialogInterface.OnClickListener() { // setItems(문자열 배열, 리스너)
                            @Override
                            public void onClick(DialogInterface dialogInterface, int which) {
                                button1.setText(versionArray[which]); // which 번째 문자로 변경
                            }
                        });
                dlg.setPositiveButton("닫기", null);
                dlg.show();
            }
        });
    }
}
```

결과 <br>

<img src="https://user-images.githubusercontent.com/96654391/170445914-571bd8c1-80c8-4bfe-a654-b4a307af82b7.png" widht="300">
<img src="https://user-images.githubusercontent.com/96654391/170445919-479c4085-5e71-41b6-890c-b07e1d6088db.png" widht="300">

### dlg.setSingleChoiceItems

-> java

```java
package com.cookandroid.exam7_14_16;

import androidx.appcompat.app.AlertDialog;
import androidx.appcompat.app.AppCompatActivity;

import android.content.DialogInterface;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        final Button button1 = (Button) findViewById(R.id.button1);
        final String[] versionArray = new String[] {"파이", "Q(10)", "R(11)"};
        button1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                AlertDialog.Builder dlg = new AlertDialog.Builder(MainActivity.this);
                 // 액티비티명.this
                dlg.setTitle("좋아하는 버전은?");
                // dlg.setMessage("이곳이 내용입니다."); 지워 줘야지 배열이 나옴
                dlg.setIcon(R.mipmap.ic_launcher);

                dlg.setSingleChoiceItems(versionArray, 0,
                        new DialogInterface.OnClickListener() {
                            @Override
                            public void onClick(DialogInterface dialogInterface, int i) {
                                button1.setText(versionArray[i]);
                            }
                        });
                dlg.setPositiveButton("닫기", null);
                dlg.show();
            }
        });
    }
}
```

결과 <br>

<img src="https://user-images.githubusercontent.com/96654391/170447539-cec473d3-c9d0-4500-a218-2928b3d04e61.png" widht="300">

### dlg.setMultiChoiceItems

-> java

```java
package com.cookandroid.exam7_14_16;

import androidx.appcompat.app.AlertDialog;
import androidx.appcompat.app.AppCompatActivity;

import android.content.DialogInterface;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        final Button button1 = (Button) findViewById(R.id.button1);
        final String[] versionArray = new String[] {"파이", "Q(10)", "R(11)"};
        final boolean[] checkArray = new boolean[] {true, false, false};
        button1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                AlertDialog.Builder dlg = new AlertDialog.Builder(MainActivity.this);
                 // 액티비티명.this
                dlg.setTitle("좋아하는 버전은?");
                // dlg.setMessage("이곳이 내용입니다."); 지워 줘야지 배열이 나옴
                dlg.setIcon(R.mipmap.ic_launcher);

                dlg.setMultiChoiceItems(versionArray, checkArray,
                        new DialogInterface.OnMultiChoiceClickListener() {
                            @Override
                            public void onClick(DialogInterface dialogInterface, int i, boolean isChecked) {
                                button1.setText(versionArray[i]);
                            }
                        });
                dlg.setPositiveButton("닫기", null);
                dlg.show();
            }
        });
    }
}
```

결과 <br>

<img src="https://user-images.githubusercontent.com/96654391/170448090-226e885f-d1d6-45ae-80d9-aff84e102c29.png" widht="300">

### 실습 7-3

색상이 들어간 토스트, 사용자 정보를 입력하는 대화상자 만들기
<br>

파일 구성

1. activity_main.xml
2. dialog1.xml
3. toast1.xml
4. MainActivity.java <br>

2번과 3번 같이 따로 xml 파일 만드는 방법

![download1](https://user-images.githubusercontent.com/96654391/170453763-8a52e6a9-e1a6-452f-b96b-81d7000cbc18.png) <br>

저기서 xml 파일 만들어 주기

<br>

실습 시작 <br>

step 1. activity_main.xml 만들어 주기

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

<br>

step 2. dialog1.xml 만들기

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

<br>

step 3. toast1.xml 만들기

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#ff0000"
    android:gravity="center">

    <!--
    <ImageView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:src="@drawable/star" /> -->

    <TextView
        android:id="@+id/toastText1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="TextView"
        android:textSize="20dp" />

    <!--
    <ImageView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:src="@drawable/star" /> -->

</LinearLayout>
```

알맞은 이미지 사진이 없어서 일단 텍스트만,,출럭하도록,,,

<br>

step 4. MainActivity.java 만들기

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
                // 대화 상자의 모양은(dialog1.xml)은 다음과 같이 불러온다.
                dialogView = (View) View.inflate(MainActivity.this, R.layout.dialog1, null);
                AlertDialog.Builder dlg = new AlertDialog.Builder(MainActivity.this);

                dlg.setTitle("사용자 정보 입력"); // 대화 상자의 제목
                dlg.setIcon(R.drawable.star); // 제목 옆에 아이콘
                dlg.setView(dialogView);
                dlg.setPositiveButton("확인", new DialogInterface.OnClickListener() {
                    @Override
                    public void onClick(DialogInterface dialogInterface, int i) {
                        // 대화상자에서의 EditText 에서 문자 가져오기
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
                        // 토스트 메시지(toast1.xml)을 불러오는 방법은 다음과 같다.
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

대화 상자의 경우는 순서를 잘 지켜서 코드를 짜야된다. + 다른 xml 파일 java에서 불러오는 방법 잘 알아두기

<br>

결과
<br>

<img src="https://user-images.githubusercontent.com/96654391/170454464-16ccf1fb-b95d-4bbe-910f-71fce1e41449.png" width="300">

<img src="https://user-images.githubusercontent.com/96654391/170454470-ecfd7d98-9b3e-43a8-ba0e-1abfe95228e6.png" width="300"> <br>

대화 상자에서 확인버튼 클릭 <br>
<img src="https://user-images.githubusercontent.com/96654391/170454490-7b514e09-02c2-44e7-a88b-a5616d7b32da.png" width="300"> <br>

대화 상자에서 취소버튼 클릭 <br>
<img src="https://user-images.githubusercontent.com/96654391/170454495-3807205e-8dff-490f-a220-cfea6e7e992d.png" width="300">
