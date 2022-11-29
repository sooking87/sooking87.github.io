---
title: "[JAVA] 병합 정렬"
excerpt: "병합 정렬"
categories: [Algorithm Study]
tags: [Algorithm Study, Java, Algorithm]
toc: true
toc_sticky: true
published: true
---

## 🔮 병합 정렬

병합 정렬이란 정렬을 마친 배열의 병합을 응용하여 분할 정복법에 따라 정렬하는 알고리즘이다. <br>
병합 정렬 과정은 먼저 배열을 앞부분과 뒷부분으로 나눈다. 정확히는 쪼개서 배열을 각각 구하는 것이 아니라 비교 자체를 center을 기준으로 비교 범위를 나눈다. -> 각 배열을 정렬한 후 병합하여 전체 정렬된 배열을 얻는다.

### 📍 병합 과정

이 과정은 데이터 구조 수업에서 배운 배열에서 다항식 sum 메소드를 구현하기 위해서 진행되었던 과정과 유사하다.

```java
// 정렬을 마친 배열 a, b를 병합하여 배열 c에 저장합니다.
    static void merge(int[] a, int na, int[] b, int nb, int[] c) {
        int pa = 0;
        int pb = 0;
        int pc = 0;

        while (pa < na && pb < nb) {
            c[pc++] = (a[pa] <= b[pb] ? a[pa++] : b[pb++]);
        }

        while (pa < na) {
            c[pc++] = a[pa++];
        }

        while (pb < nb) {
            c[pc++] = b[pb++];
        }
    }
```

- a, b : 병합이 필요한 두 배열
- c : 정렬된 요소가 들어갈 배열
- na, nb : 배열의 전체 크기
- pa, pb : 비교해야될 요소가 들어있는 인덱스
- pc : c 배열에 들어가야 되는 인덱스

### 📍 병합 정렬

```java
import java.util.Scanner;

public class MerygeSort {
    static int[] buff;

    // a[left] ~ a[right]를 재귀적으로 병합 정렬
    static void __mergeSort(int[] a, int left, int right) {
        if (left < right) {
            int i;
            int center = (left + right) / 2;
            int p = 0;
            int j = 0;
            int k = left;

            __mergeSort(a, left, center);
            __mergeSort(a, center + 1, right);

            // 왼쪽 배열 buff 배열에 복사
            for (i = left; i <= center; i++) {
                buff[p++] = a[i];
            }

            // 왼쪽 배열 + 오른쪽 배열 정렬
            while (i <= right && j < p) {
                a[k++] = (buff[j] <= a[i]) ? buff[j++] : a[i++];
            }

            // buff 배열의 나머지 요소를 a 배열에 복사 -> buff 배열에 남는 경우 == 뒷부분 배열보다 큰 값이 들어있는 경우
            while (j < p) {
                a[k++] = buff[j++];
            }
        }
    }

    // 병합 정렬
    static void mergeSort(int[] a, int n) {
        buff = new int[n]; // 작업용 배열을 생성
        __mergeSort(a, 0, n - 1); // 배열 전체를 병합 정렬

        buff = null; // 작업용 배열 해제
    }
}
```

병합 정렬은 메인에서 _mergeSort()_ 메소드를 호출하면서 시작된다.

- 변수 및 배열 역할
  - left : 왼쪽 배열의 최대 인덱스
  - right : 오른쪽 배열의 최대 인덱스
  - buff : 작업용 배열
  - p : 0부터 시작하여 buff 배열에 a 배열을 복사 -> 반복문 끝나면 p는 center - left + 1를 나타냄 -> 다음 반복문에서 j 반복 범위를 지정
  - i : left부터 시작하여 중간값까지 buff 배열에 넣기 위한 인덱스 -> 반복문 끝나면 i는 center - left + 1를 나타냄 -> 다음 반복문에서 뒷부분 배열 직접 접근 핸들링에 사용
  - j : buff에 들어있는 a 배열 앞부분을 접근하기 위한 인덱스
  - k : 0부터 시작하여 a + b 배열을 넣기 위한 인덱스

배열의 비교, 배열에 저장 시간 복잡도는 O(n)이고 데이터의 요소 개수가 n개일 때, 병합 정렬의 단계는 log n만큼 필요, n개의 배열이 이동하는데 2 \* log<sub>2</sub>n번 수행-> **_nlog₂n(비교) + 2nlog₂n(이동) -> O(nlogn)_** 복잡도를 가짐.

❓ 왜 logn시간 복잡도를 가질까,,? <br>

💡 n개의 요소가 있다고 가정할 때, 절반으로 쪼개면서 요소의 비교, 이동, 합병이 이루어진다. 여기서 병합 시간 복잡도가 O(n)이었던 것이고, 병합 정렬의 단계에서 n개의 요소라면 2개씩 분할되어 2^k번 수행이되고, 얘를 다시 병합하기 위해서는 k = log<sub>2</sub>n만큼 필요하다.

## 🔮 Arrays.sort로 퀵 정렬과 병합 정렬하기

### 📍 단순 오름차순(퀵 정렬)

```java
package MergeSort;

import java.util.Arrays;
import java.util.Scanner;

public class ArraySortTest {
    public static void main(String[] args) {
        Scanner stdIn = new Scanner(System.in);

        System.out.print("요솟수: ");
        int num = stdIn.nextInt();
        int[] x = new int[num];

        for (int i = 0; i < num; i++) {
            System.out.println("x[" + i + "]: ");
            x[i] = stdIn.nextInt();
        }

        Arrays.sort(x);

        System.out.println("오름차순 완료");
        for (int i = 0; i < num; i++) {
            System.out.println("x[" + i + "] = " + x[i]);
        }
    }
}
```

### 📍 병합 정렬

▶️ 자연 정렬

```java
package MergeSort;

import java.util.Arrays;
import java.util.Calendar;
import java.util.GregorianCalendar;

public class SortCalendar {
    public static void main(String[] args) {
        GregorianCalendar[] x = {
                new GregorianCalendar(2017, 11, 1),
                new GregorianCalendar(1963, 10, 18),
                new GregorianCalendar(1985, 4, 5)
        };

        Arrays.sort(x);

        for (int i = 0; i < x.length; i++) {
            System.out.printf("%04d년 %02d월 %02d일\n",
                    x[i].get(Calendar.YEAR),
                    x[i].get(Calendar.MONTH) + 1,
                    x[i].get(Calendar.DATE));
        }
        ;
    }
}
```

<br>
▶️ 메서드로 정렬

신체검사 데이터를 받을 클래스 생성 -> PhyscData 클래스 생성

```java
static class PhyscData {
    String name;
    int height;
    double vision;

    // 생성자
    PhyscData(String name, int height, double vision) {
        this.name = name;
        this.height = height;
        this.vision = vision;
    }

    public String toString() {
        return name + " " + height + " " + vision;
    }

    //?
    static final Comparator<PhyscData> HEIGHT_ORDER = new HeightOrderComparator();

    private static class HeightOrderComparator implements Comparator<PhyscData> {
        public int compare(PhyscData d1, PhyscData d2) {
            return (d1.height > d2.height) ? 1 : (d1.height < d2.height ? -1 : 0);
        }
    }
```

,,,,,,❓
