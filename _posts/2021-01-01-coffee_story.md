---
layout: post
title:  "COFFEE 이야기"
---

# 첫 웹 사이트 제작기

앞으로 어떻게 블로그를 사용해야되며, CSS와 html, 웹 사이트에 사용된 사진 등을 어떻게 올려야 되는지 공부를 해야겠다. 


<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>커피 이야기</title>
    
    <style media="screen">
    .title {
      font-size: 30px;
      text-align: center;
      width: 100%;
      border: 5px solid #4E4545;
      margin: 5px;
    }
    .first, .second, .last {
      border: 5px solid #4E4545;
      margin: 5px;
      width:100%;
      display:grid;
      grid-template-columns: 2fr 6fr 3fr;
      grid-template-rows: minmax(100px, auto);
    }

    h3 {
      font-size: 25px;
    }
    p {
      font-size: 20px;
    }
    ol {
      font-size: 20px;
    }
    * {
      font-family: 'Gaegu', cursive;
    }
    body {
      background-color: #897A7A;
    }
    a {
      text-decoration: none;
      color: #312222;
    }
    </style>
  </head>

  <body>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Gaegu:wght@300&display=swap" rel="stylesheet">

<div class="title">
  <h1>COFFEE 이야기</h1>
</div>

<div class="first">
    <h3 style=text-align:center>커피 유래</h3>
    <p><strong>커피</strong>는 7세기 이전부터 에티오피아의 고대에서 자생하고 있던 것으로 보인다. 전설에 따르면 염소 목이었던 칼디(Kaldi)가 우연히 염소들이 먹던 열매를 발견했고 매를 마을에 가져오는데, 피곤함을 덜어주는 <strong>커피</strong>의 효능을 마을의 종교 수행자들을 돕기 위해 쓰게 되다고 전해지고 있다.</p>
    <img src="coffee.jpg" width="100%">
</div>

<div class="second">
    <h3 style=text-align:center>원두 종류</h3>
    <ol>
      <li><a href="아라비카.html">아라비카</a></li>
      <li><a href="로브스타.html">로브스타</a></li>
      <li><a href="리베리카.html">리베리카</a></li>
    </ol>
    <img src="coffee2.jpg" width="100%">
</div>

<div class="last">
    <h3 style=text-align:center>커피 종류</h3>
    <ol>
      <li><a href="에스프레소.html">에스프레소</a></li>
      <li><a href="아메리카노.html">아메리카노</a></li>
      <li><a href="카페라테.html">카페라테</a></li>
      <li><a href="마키아토.html">마키아토</a></li>
      <li><a href="카페모카.html">카페모카</a></li>
      <li><a href="아포카토.html">아포카토</a></li>
    </ol>
    <img src="coffee3.jpg" width="100%">
</div>
<p style=text-align:center>더 궁금한 사항이 있으면 <strong>댓글</strong> 또는 우측하단의 <strong>채팅 기능</strong>을 사용해주세요!</p>
    <div id="disqus_thread"></div>
<script>
    /**
    *  RECOMMENDED CONFIGURATION VARIABLES: EDIT AND UNCOMMENT THE SECTION BELOW TO INSERT DYNAMIC VALUES FROM YOUR PLATFORM OR CMS.
    *  LEARN WHY DEFINING THESE VARIABLES IS IMPORTANT: https://disqus.com/admin/universalcode/#configuration-variables    */
    /*
    var disqus_config = function () {
    this.page.url = PAGE_URL;  // Replace PAGE_URL with your page's canonical URL variable
    this.page.identifier = PAGE_IDENTIFIER; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
    };
    */
    (function() { // DON'T EDIT BELOW THIS LINE
    var d = document, s = d.createElement('script');
    s.src = 'https://coffee-story-1.disqus.com/embed.js';
    s.setAttribute('data-timestamp', +new Date());
    (d.head || d.body).appendChild(s);
    })();
</script>

<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
<!--Start of Tawk.to Script-->
<script type="text/javascript">
var Tawk_API=Tawk_API||{}, Tawk_LoadStart=new Date();
(function(){
var s1=document.createElement("script"),s0=document.getElementsByTagName("script")[0];
s1.async=true;
s1.src='https://embed.tawk.to/61c6c75780b2296cfdd3be4d/1fno7lc3e';
s1.charset='UTF-8';
s1.setAttribute('crossorigin','*');
s0.parentNode.insertBefore(s1,s0);
})();
</script>
<!--End of Tawk.to Script-->
  </body>
</html>
<!--
http://paletton.com/#uid=1000u0k2ljc6hnI3vhb50fr6wdx 밝은 계열
http://paletton.com/#uid=1000u0k3i7H4mcB3L9O4O7c9y6a 어두운 계열
-->

