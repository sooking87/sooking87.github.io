---
title: "[Section 02] CSS 3D #3"
excerpt: "[Section 02] CSS 3D #3"
categories: [Interactive Web]
tags: [Interactive Web, WEB]
toc: true
toc_sticky: true
---

# CSS 3D

## 🔮 CSS 3D #3

인터넷 별로 표준 스타일이 아닌 새로 나온 속성인 경우 다음과 같이 해준다.

```css
-webkit-backface-visibility: hidden; /* 크롬 & 사파리 */
-moz-backface-visibility: hidden; /* 모질라 */
-o-backface-visibility: hidden; /* 오페라 */
backface-visibility: hidden; /* 표준 스타일 */
```

표준 스타일을 제일 아래 다시 적어주는 것이 좋다. 최종적으로 표준 스타일이 적용되는 경우가 있을 수 있기 때문.
<br>

음 그리고,, 인터넷 익스플로러에서도 적용되는 방법을 알려주었는데, 인터넷 익스플로러는 서비스가 종료되었다고 알고 있기 때문에 딱히 필요 없을 것 같음,,,,,,,아마두?
