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

## 웹뷰
