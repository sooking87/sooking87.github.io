---
title: "14.2주차"
excerpt: "14.2주차"
categories: [Android Studio]
tags: [Android Studio, Java]
toc: true
toc_sticky: true
---

📌시험범위는 아닌 것 같음.
# chap.09 그래픽과 이미지

- 캔버스에 도형을 그리는 방법을 익힌다. 

## 그래픽

## 캔버스와 페인트 기본

- Canvas 클래스

점, 선, 원, 사각형 그리기 / 텍스트 쓰기 / 이미지 출력 <br>

도화지 개념

- Paint 클래스

색상 선택 / 스타일 선택 / 펜 두께 선택 / 글꼴 선택 <br>

붓 개념

```java
package com.cookandroid.draw09;

import androidx.appcompat.app.AppCompatActivity;

import android.content.Context;
import android.graphics.Canvas;
import android.graphics.Color;
import android.graphics.Paint;
import android.graphics.Path;
import android.graphics.Rect;
import android.graphics.RectF;
import android.os.Bundle;
import android.view.View;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(new MyGraphicsView(this));
    }
    private static class MyGraphicsView extends View {
        public MyGraphicsView(Context context) {
            super(context);
        }

        @Override
        protected void onDraw(Canvas canvas) {
            super.onDraw(canvas);
            Paint paint = new Paint();
            paint.setAntiAlias(true);
            paint.setColor(Color.GREEN);
            canvas.drawLine(10, 10, 300, 10, paint);

            paint.setColor(Color.BLUE);
            paint.setStrokeWidth(5);
            canvas.drawLine(10, 30, 300, 30, paint);

            paint.setColor(Color.RED);
            paint.setStrokeWidth(0);

            paint.setStyle(Paint.Style.FILL);
            Rect rect1 = new Rect(10, 120, 10 + 100, 120 + 100);
            canvas.drawRect(rect1, paint);

            paint.setStyle(Paint.Style.STROKE);
            Rect rect2 = new Rect(130, 120, 130 + 100, 120+100);
            canvas.drawRect(rect2, paint);

            RectF rect3 = new RectF(250, 120, 250+100, 120+100);
            canvas.drawRoundRect(rect3, 20, 20, paint);

            paint.setColor(Color.BLUE);
            paint.setStrokeWidth(5);
            canvas.drawCircle(60, 320, 50, paint);

            paint.setColor(Color.CYAN);
            paint.setStrokeWidth(5);
            Path path1 = new Path();
            path1.moveTo(10, 400);
            path1.lineTo(10 + 50, 400+50);
            path1.lineTo(10 + 100, 400);
            path1.lineTo(10 + 150, 400 + 50);
            path1.lineTo(10 + 200, 400);
            canvas.drawPath(path1, paint);

            paint.setColor(Color.MAGENTA);
            paint.setStrokeWidth(5);
            paint.setTextSize(50);
            canvas.drawText("안드로이드", 10, 550, paint);
            
        }
    }

}
```

## 결과

<img width="316" alt="화면 캡처 2022-05-10 141221" src="https://user-images.githubusercontent.com/96654391/172329571-b3f3c7d7-e361-41b5-affc-78fe7f860ebb.png">

## 그래픽 처리 기본

```java
package com.cookandroid.draw09;

import androidx.appcompat.app.AppCompatActivity;

import android.content.Context;
import android.graphics.Canvas;
import android.graphics.Color;
import android.graphics.Paint;
import android.graphics.Path;
import android.graphics.Rect;
import android.graphics.RectF;
import android.os.Bundle;
import android.view.View;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(new MyGraphicsView(this));
    }
    private static class MyGraphicsView extends View {
        public MyGraphicsView(Context context) {
            super(context);
        }

        @Override
        protected void onDraw(Canvas canvas) {
            super.onDraw(canvas);
            Paint paint = new Paint();
            paint.setAntiAlias(true);
            paint.setColor(Color.BLACK);
            paint.setStrokeWidth(60);
            canvas.drawLine(60, 60, 600, 60, paint);
            
            paint.setStrokeCap(Paint.Cap.ROUND);
            canvas.drawLine(60, 160, 600, 160, paint);

            RectF rectF = new RectF();
            rectF.set(120, 240, 120+ 400, 200+200);
            canvas.drawOval(rectF, paint);


            rectF.set(120, 340, 120+200, 340 + 200);
            canvas.drawArc(rectF, 40, 110, true, paint);

            paint.setColor(Color.BLUE);
            rectF.set(120, 560, 120+200, 560+200);
            canvas.drawRect(rectF, paint);

            paint.setColor(Color.argb(88, 0xff, 00, 00));
            rectF.set(180, 620, 180+200, 620 + 200);
            canvas.drawRect(rectF, paint);



        }
    }

}
```

## 결과

<img width="303" alt="화면 캡처 2022-05-10 141221" src="https://user-images.githubusercontent.com/96654391/172332730-970ba794-b74a-474b-9db5-a13694035eee.png">
