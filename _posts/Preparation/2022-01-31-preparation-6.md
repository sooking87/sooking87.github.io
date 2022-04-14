---
title: "[WEB] Node.js를 통해 파일 읽기"
excerpt: "[WEB] Node.js를 통해 파일 읽기"
categories: [Preparation]
tags: [Preparation, WEB, HTML/CSS/Javascript]
toc: true
toc_sticky: true
---

## 1차적인 html/css틀 만들기

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="JjOGGJZ" data-user="sooking87" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/sooking87/pen/JjOGGJZ">
  project 3</a> by sohnsookyoung (<a href="https://codepen.io/sooking87">@sooking87</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

## Node.js로 사진 불러오기: readFile()

<div class="colorscripter-code" style="color:#f0f0f0;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px;border-right:2px solid #4f4f4f"><div style="margin:0;padding:0;word-break:normal;text-align:right;color:#aaa;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="line-height:130%">1</div><div style="line-height:130%">2</div><div style="line-height:130%">3</div><div style="line-height:130%">4</div><div style="line-height:130%">5</div><div style="line-height:130%">6</div><div style="line-height:130%">7</div><div style="line-height:130%">8</div><div style="line-height:130%">9</div><div style="line-height:130%">10</div><div style="line-height:130%">11</div><div style="line-height:130%">12</div><div style="line-height:130%">13</div><div style="line-height:130%">14</div><div style="line-height:130%">15</div></div></td><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#f0f0f0;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#ff3399">var</span>&nbsp;http&nbsp;<span style="color:#aaffaa"></span><span style="color:#ff3399">=</span>&nbsp;require(<span style="color:#ffd500">'http'</span>)</div><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#ff3399">var</span>&nbsp;fs&nbsp;<span style="color:#aaffaa"></span><span style="color:#ff3399">=</span>&nbsp;require(<span style="color:#ffd500">'fs'</span>)</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;</div><div style="padding:0 6px; white-space:pre; line-height:130%">fs.readFile(<span style="color:#ffd500">'./images/sample2.jpg'</span>,&nbsp;<span style="color:#ff3399">function</span>(err,&nbsp;data)&nbsp;{</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;<span style="color:#ff3399">if</span>&nbsp;(err)&nbsp;<span style="color:#ff3399">throw</span>&nbsp;err&nbsp;<span style="color:#999999">//&nbsp;Fail&nbsp;if&nbsp;the&nbsp;file&nbsp;can't&nbsp;be&nbsp;read.</span></div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;http.createServer(<span style="color:#ff3399">function</span>(req,&nbsp;res)&nbsp;{</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;res.writeHead(<span style="color:#c10aff">200</span>,&nbsp;{<span style="color:#ffd500">'Content-Type'</span>:&nbsp;<span style="color:#ffd500">'text/html'</span>});</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;res.write(<span style="color:#ffd500">'&lt;html&gt;&lt;body&gt;&lt;img&nbsp;width="300px"&nbsp;height="400px"&nbsp;src="data:image/jpeg;base64,'</span>)</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;res.write(Buffer.<span style="color:#ff3399">from</span>(data).toString(<span style="color:#ffd500">'base64'</span>));</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;res.end(<span style="color:#ffd500">'"/&gt;&lt;/body&gt;&lt;/html&gt;'</span>);</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#999999">//res.end(data)&nbsp;//&nbsp;Send&nbsp;the&nbsp;file&nbsp;data&nbsp;to&nbsp;the&nbsp;browser.</span></div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;}).listen(<span style="color:#c10aff">3000</span>)</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;<span style="color:#4be6fa">console</span>.log(<span style="color:#ffd500">'Server&nbsp;running&nbsp;at&nbsp;http://localhost:3000/'</span>)</div><div style="padding:0 6px; white-space:pre; line-height:130%">})</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;</div></div><div style="text-align:right;margin-top:-13px;margin-right:5px;font-size:9px;font-style:italic"><a href="http://colorscripter.com/info#e" target="_blank" style="color:#4f4f4ftext-decoration:none">Colored by Color Scripter</a></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#4f4f4f;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div>

`fs.readFile(경로, function(err, data))`

<ul>
  <li>경로에서 읽은 파일을 data로 이동시켜서 브라우저로 값을 보냄</li>
</ul>

`res.writeHead(statusCode, statusMessage, headers)`

<ul>
  <li>statusCode: 숫자 유형의 상태코드, 200-정상, 404-에러</li>
  <li>statusMessae: **Content-Type** 이 **text/html** 이라는 것을 알려줌</li>
  <li>header: 함수, 배열, 문자열 자리</li>
</ul>

`res.write()`

<ul>
  <li>괄호 안의 컨텐츠를 보낸다.</li>
</ul>

`res.end()`

<ul>
  <li>콘텐츠 출력을 완료한다.</li>
</ul>

## 폴더에서 파일 리스트 가져오기: readdir()

<div class="colorscripter-code" style="color:#f0f0f0;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px;border-right:2px solid #4f4f4f"><div style="margin:0;padding:0;word-break:normal;text-align:right;color:#aaa;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="line-height:130%">1</div><div style="line-height:130%">2</div><div style="line-height:130%">3</div><div style="line-height:130%">4</div><div style="line-height:130%">5</div><div style="line-height:130%">6</div><div style="line-height:130%">7</div></div></td><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#f0f0f0;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#ff3399">const</span>&nbsp;testFolder&nbsp;<span style="color:#aaffaa"></span><span style="color:#ff3399">=</span>&nbsp;<span style="color:#ffd500">'./images'</span>;</div><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#ff3399">const</span>&nbsp;fs&nbsp;<span style="color:#aaffaa"></span><span style="color:#ff3399">=</span>&nbsp;require(<span style="color:#ffd500">'fs'</span>);</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;</div><div style="padding:0 6px; white-space:pre; line-height:130%">fs.readdir(testFolder,&nbsp;<span style="color:#ff3399">function</span>(error,&nbsp;filelist){</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;<span style="color:#4be6fa">console</span>.log(filelist);</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;<span style="color:#4be6fa">console</span>.log(filelist.<span style="color:#4be6fa">length</span>);</div><div style="padding:0 6px; white-space:pre; line-height:130%">})</div></div><div style="text-align:right;margin-top:-13px;margin-right:5px;font-size:9px;font-style:italic"><a href="http://colorscripter.com/info#e" target="_blank" style="color:#4f4f4ftext-decoration:none">Colored by Color Scripter</a></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#4f4f4f;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div>

`fs.readdir(경로, function(err, filelist))`

<ul>
  <li>filelist안에 폴더 경로에 있는 파일들을 모두 리스트 형식으로 출력한다. .length를 통해서 개수도 알 수 있다.</li>
</ul>

## 폴더에서 경로 가져오기: path.basename()

<div class="colorscripter-code" style="color:#f0f0f0;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px;border-right:2px solid #4f4f4f"><div style="margin:0;padding:0;word-break:normal;text-align:right;color:#aaa;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="line-height:130%">1</div><div style="line-height:130%">2</div><div style="line-height:130%">3</div><div style="line-height:130%">4</div><div style="line-height:130%">5</div><div style="line-height:130%">6</div><div style="line-height:130%">7</div><div style="line-height:130%">8</div></div></td><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#f0f0f0;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#ff3399">var</span>&nbsp;path&nbsp;<span style="color:#aaffaa"></span><span style="color:#ff3399">=</span>&nbsp;require(<span style="color:#ffd500">'path'</span>);</div><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#ff3399">var</span>&nbsp;fileName&nbsp;<span style="color:#aaffaa"></span><span style="color:#ff3399">=</span>&nbsp;<span style="color:#ffd500">"./images/sample.jpg"</span>;</div><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#ff3399">var</span>&nbsp;dirName&nbsp;<span style="color:#aaffaa"></span><span style="color:#ff3399">=</span>&nbsp;path.dirname(fileName);</div><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#ff3399">var</span>&nbsp;baseName&nbsp;<span style="color:#aaffaa"></span><span style="color:#ff3399">=</span>&nbsp;path.basename(fileName);</div><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#ff3399">var</span>&nbsp;extName&nbsp;<span style="color:#aaffaa"></span><span style="color:#ff3399">=</span>&nbsp;path.extname(fileName);</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;</div><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#4be6fa">console</span>.log(path);</div><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#4be6fa">console</span>.log(<span style="color:#ffd500">"디렉토리:&nbsp;%s,&nbsp;파일이름:&nbsp;%s,&nbsp;확장자:&nbsp;%s"</span>,&nbsp;dirName,&nbsp;baseName,&nbsp;extName);</div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#4f4f4f;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div>

앞에서 **readdir()** 을 통해서 파일 리스트를 가져온 후 `filelist[i]` 를 통해서 하나씩 **readFile()** 을 이용하여 **respnse.write** 를 하면 되는 줄 알았으나, **readdir** 에는 파일의 경로가 필요하지만 **readFile** 을 통해서 정확한 경로가 들어가지 않는 것 같았다. 구체적으로 ./images/undefined라고 뜬다. 그래서 **path.basename** 을 통해서 파일의 경로를 찾아서 **readFile()** 에 넣을 예정이다.

## 수정할 사항

1. 보다시피 화면 크기에 따른 배치를 진행하지 않았다.
2. Node.js를 통해서 `images` 폴더에 사진을 추가만 하면 알아서 출력될 수 있도록 해야된다. 그러면 파일 경로에 해당하는 매개변수를 어떻게 처리해야될지도 알아봐야겠다.
3. 2번의 연장선에서 사진이 추가될 때마다 사진을 원하는 모양, 위치에 추가시킬 수 있도록 해야겠다.
