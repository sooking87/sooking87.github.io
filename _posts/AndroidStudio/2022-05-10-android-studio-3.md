---
title: "이벤트 처리 벼락"
excerpt: "이벤트 처리 벼락"
categories: [Android Studio]
tags: [Android Studio, Java]
toc: true
toc_sticky: true
---

-> xml

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical" >

    <EditText
        android:id="@+id/edit1"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="입력 하세요"/ >

    <Button
        android:id="@+id/btnToast"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="글자 나타내기" />

    <Button
        android:id="@+id/btnHomepage"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="홈페이지 열기" />

    <RadioGroup
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center" >

        <RadioButton
            android:id="@+id/rdoR"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:checked="true"
            android:text="11.0(R)" />

        <RadioButton
            android:id="@+id/rdoS"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="12.0(S)" />

    </RadioGroup>

    <ImageView
        android:id="@+id/ivAndroid"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center"
        android:src="@drawable/r" />

</LinearLayout>
```

<br>

-> java

```java
package com.cookandroid.test007;

import androidx.appcompat.app.AppCompatActivity;
import android.content.Intent;
import android.net.Uri;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.ImageView;
import android.widget.RadioButton;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {
    EditText edit1;
    Button btnToast, btnHomepage;
    RadioButton rdoR, rdoS;
    ImageView ivAndroid;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // 필요한거 아이디 불러오기
        setTitle("좀 그럴듯한 앱");
        edit1 = (EditText) findViewById(R.id.edit1);
        btnToast = (Button) findViewById(R.id.btnToast);
        btnHomepage = (Button) findViewById(R.id.btnHomepage);
        rdoR = (RadioButton) findViewById(R.id.rdoR);
        rdoS = (RadioButton) findViewById(R.id.rdoS);
        ivAndroid = (ImageView) findViewById(R.id.ivAndroid);

        // EditText에 입력한 글자가 잠깐 Toast 메시지로 출력
        btnToast.setOnClickListener(new View.OnClickListener() {
            public void onClick(View v) {
            Toast.makeText(getApplicationContext(),
            edit1.getText().toString(), Toast.LENGTH_SHORT).show();
            }
        });

        // <홈페이지 열기>를 클릭하면 EditText에 입력한 URL이 열린다
        btnHomepage.setOnClickListener(new View.OnClickListener() {
            public void onClick(View v) {
            Intent mIntent = new Intent(Intent.ACTION_VIEW, Uri.parse(edit1
            .getText().toString()));
            startActivity(mIntent);
            }
        });

        // 처음에는 기본 이미지가, 라디오버튼을 클릭하면 다른 이미지로 변경된다
        rdoR.setOnClickListener(new View.OnClickListener() {
            public void onClick(View v) {
            ivAndroid.setImageResource(R.drawable.r);
            }
        });
        rdoS.setOnClickListener(new View.OnClickListener() {
            public void onClick(View v) {
            ivAndroid.setImageResource(R.drawable.s);
            }
        });
    }
}
```
