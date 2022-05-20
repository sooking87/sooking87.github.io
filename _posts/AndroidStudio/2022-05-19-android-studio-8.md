---
title: "12.1주차"
excerpt: "12.1주차"
categories: [Android Studio]
tags: [Android Studio, Java]
toc: true
toc_sticky: true
---

# 뷰 컨테이너

## 탭 호스트

여러 탭을 두고 각 탭을 클릭할 때마다 해당 화면이 나오도록 설정하는 뷰 컨테이너 <br>

주의 ! 탭 호스트, 탭 위젯, 프레임 레이아웃의 id가 지정되어 있는데 **_변경하지 말고 그대로 사용_** 해야 안드로이드가 탭호스트의 구성을 인식

- id="@android:id/tabhost"
- id="@android:id/tabs"
- id="@android:id/tabcontent"
  <br>

- 탭스팩은 택을 구성하는 요소들의 집합
- 탭스펙 : 탭을 구성하는 요소들의 집합, 탭호스트를 처리할 때 고정된 형식의 코드
  <br>

-> xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<TabHost xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@android:id/tabhost"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <LinearLayout
        android:id="@+id/linearLayout1"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">

        <TabWidget
            android:id="@android:id/tabs"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"></TabWidget>
        <FrameLayout
            android:id="@android:id/tabcontent"
            android:layout_width="match_parent"
            android:layout_height="match_parent">

            <LinearLayout
                android:id="@+id/tabSong"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:orientation="vertical"
                android:background="#ff0000"></LinearLayout>

            <LinearLayout
                android:id="@+id/tabArtist"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:orientation="vertical"
                android:background="#00ff00"></LinearLayout>

            <LinearLayout
                android:id="@+id/tabAlbum"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:orientation="vertical"
                android:background="#0000ff"></LinearLayout>
        </FrameLayout>

    </LinearLayout>


</TabHost>
```

<br>

-> java

```java
package com.cookandroid.tabhost;

import androidx.appcompat.app.AppCompatActivity;

import android.app.TabActivity;
import android.os.Bundle;
import android.widget.TabHost;

import com.google.android.material.tabs.TabLayout;

public class MainActivity extends TabActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        TabHost tabHost = getTabHost();
        // 탭호스트 생성
        TabHost.TabSpec tabSpecSong = tabHost.newTabSpec("SONG").setIndicator("음악별");
        tabSpecSong.setContent(R.id.tabSong);
        tabHost.addTab(tabSpecSong);

        TabHost.TabSpec tabSpecAritist = tabHost.newTabSpec("ARTIST").setIndicator("가수별");
        tabSpecAritist.setContent(R.id.tabArtist);
        tabHost.addTab(tabSpecAritist);

        TabHost.TabSpec tabSpecAlbum = tabHost.newTabSpec("ALBUM").setIndicator("앨범별");
        tabSpecAlbum.setContent(R.id.tabAlbum);
        tabHost.addTab(tabSpecAlbum);


    }
}
```

<img src="https://user-images.githubusercontent.com/96654391/169244352-5b5f99d9-eb03-494f-b74b-988b5e45b283.png" width="300">

## 액션바

관련 내용에 대한 실습은 생략

## 프래그먼트

관련 내용에 대한 실습은 생략

## 웹뷰

사용자가 웹브라우저 기능을 앱 안에서 직접 포함할 수 있는 위젯이다. 웹뷰를 실제 웹브라우저처럼 만들려면 많은 작업이 필요하다. <br>

- AndroidManifest.xml 파일에 퍼미션을 지정해야 하는데 인터넷을 사용하는 프로젝트마다 AndroidManifest.xml > `<uses-permission android:name="android.permission.INTERNET" />`을 추가해야된다.
  <br>

-> AndroidManifest.xml : 수정이 필요함. `<uses-permission android:name="android.permission.INTERNET" />`을 추가 + 뭔지 모르겠지만 application 부분에도 `android:usesCleartextTraffic="true"`를 추가해주어야 됨. 자세한 이유는 모름!

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.cookandroid.project6_2">

    <uses-permission android:name="android.permission.INTERNET" />

    <application
        android:allowBackup="true"
        android:icon="@drawable/emo_im_laughing"
        android:label="@string/app_name"
        android:logo="@drawable/web"
        android:theme="@style/Theme.AppCompat.Light.DarkActionBar"
        android:usesCleartextTraffic="true">
        <activity
            android:name=".MainActivity"
            android:label="간단 웹브라우저"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>
```

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <LinearLayout
        android:id="@+id/linearLayout1"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal">
        <EditText
            android:id="@+id/edtUrl1"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:hint="URL을 입력하세요."
            android:singleLine="true"></EditText>

        <Button
            android:id="@+id/btnGo"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="이동"></Button>

        <Button
            android:id="@+id/btnBack"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="이전"></Button>
    </LinearLayout>

    <WebView
        android:id="@+id/webView1"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:clickable="true"></WebView>

</LinearLayout>
```

<br>
-> java

```java
package com.cookandroid.project6_2;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.View;
import android.webkit.WebSettings;
import android.webkit.WebView;
import android.webkit.WebViewClient;
import android.widget.Button;
import android.widget.EditText;

public class MainActivity extends AppCompatActivity {

    EditText edtUrl;
    Button btnGo, btnBack;
    WebView web;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);


        edtUrl = (EditText) findViewById(R.id.edtUrl1);
        btnGo = (Button) findViewById(R.id.btnGo);
        btnBack = (Button) findViewById(R.id.btnBack);
        web = (WebView) findViewById(R.id.webView1);

        // 새 창 띄우기 않기
        web.setWebViewClient((new CookWebViewClient()));

        // 세부 세팅 등록
        WebSettings webSet = web.getSettings();
        // 화면 확대 축소 허용 여부 버튼
        webSet.setBuiltInZoomControls(true);
        // 자바 스크립트 허용 여부
        webSet.setJavaScriptEnabled(true);

        btnGo.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                web.loadUrl(edtUrl.getText().toString());
            }
        });

        btnBack.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                web.goBack();
            }
        });
    }

    class CookWebViewClient extends WebViewClient {

        @Override
        public boolean shouldOverrideUrlLoading(WebView view, String url) {
            return super.shouldOverrideUrlLoading(view, url);
        }

    }

}
```

이를 구현시키기 위해서는 WebView 클래스 뿐 아니라 **_CookWebViewClient_** 라는 클래스를 정의하고(onCreate 바깥에), 이 클래스를 활용하여 새 창을 띄우지 않기 위해서(webView 위치에 네이버 창을 넣기 위해서) 설정해주어야 한다.(`web.setWebViewClient((new CookWebViewClient()));`) -> **_loadUrl(), goBack()_** 사용

<img src="https://user-images.githubusercontent.com/96654391/169580145-ac8165bc-84e1-4a18-bfc5-e06dacc7ac86.png" width="300">

<img src="https://user-images.githubusercontent.com/96654391/169580150-5ef36a87-4e72-435b-ba76-57c42f483dba.png" width="300">
