---
title: "[백준 1292번] 쉽게 푸는 문제"
excerpt: "[백준 1292번] 쉽게 푸는 문제"
categories: [Backjoon Java]
tags: [Backjoon, Java]
toc: true
toc_sticky: true
---

## [백준 1292번] 쉽게 푸는 문제

<div class="colorscripter-code" style="color:#f0f0f0;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px;border-right:2px solid #4f4f4f"><div style="margin:0;padding:0;word-break:normal;text-align:right;color:#aaa;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="line-height:130%">1</div><div style="line-height:130%">2</div><div style="line-height:130%">3</div><div style="line-height:130%">4</div><div style="line-height:130%">5</div><div style="line-height:130%">6</div><div style="line-height:130%">7</div><div style="line-height:130%">8</div><div style="line-height:130%">9</div><div style="line-height:130%">10</div><div style="line-height:130%">11</div><div style="line-height:130%">12</div><div style="line-height:130%">13</div><div style="line-height:130%">14</div><div style="line-height:130%">15</div><div style="line-height:130%">16</div><div style="line-height:130%">17</div><div style="line-height:130%">18</div><div style="line-height:130%">19</div><div style="line-height:130%">20</div><div style="line-height:130%">21</div><div style="line-height:130%">22</div><div style="line-height:130%">23</div><div style="line-height:130%">24</div><div style="line-height:130%">25</div><div style="line-height:130%">26</div><div style="line-height:130%">27</div><div style="line-height:130%">28</div><div style="line-height:130%">29</div><div style="line-height:130%">30</div><div style="line-height:130%">31</div><div style="line-height:130%">32</div><div style="line-height:130%">33</div><div style="line-height:130%">34</div><div style="line-height:130%">35</div></div></td><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#f0f0f0;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#ff3399">import</span>&nbsp;java.io.BufferedReader;</div><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#ff3399">import</span>&nbsp;java.io.BufferedWriter;</div><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#ff3399">import</span>&nbsp;java.io.IOException;</div><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#ff3399">import</span>&nbsp;java.io.InputStreamReader;</div><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#ff3399">import</span>&nbsp;java.io.OutputStreamWriter;</div><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#ff3399">import</span>&nbsp;java.util.StringTokenizer;</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;</div><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#ff3399">public</span>&nbsp;<span style="color:#ff3399">class</span>&nbsp;백준_손수경_정답_1292&nbsp;{</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#ff3399">public</span>&nbsp;<span style="color:#ff3399">static</span>&nbsp;<span style="color:#ff3399">void</span>&nbsp;main(<span style="color:#4be6fa">String</span>[]&nbsp;args)&nbsp;<span style="color:#ff3399">throws</span>&nbsp;IOException&nbsp;{</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;BufferedReader&nbsp;br&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">=</span>&nbsp;<span style="color:#ff3399">new</span>&nbsp;BufferedReader(<span style="color:#ff3399">new</span>&nbsp;InputStreamReader(<span style="color:#4be6fa">System</span>.<span style="color:#4be6fa">in</span>));</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;BufferedWriter&nbsp;bw&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">=</span>&nbsp;<span style="color:#ff3399">new</span>&nbsp;BufferedWriter(<span style="color:#ff3399">new</span>&nbsp;OutputStreamWriter(<span style="color:#4be6fa">System</span>.<span style="color:#4be6fa">out</span>));</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;StringTokenizer&nbsp;st&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">=</span>&nbsp;<span style="color:#ff3399">new</span>&nbsp;StringTokenizer(br.readLine());</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#4be6fa">int</span>[]&nbsp;arr&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">=</span>&nbsp;<span style="color:#ff3399">new</span>&nbsp;<span style="color:#4be6fa">int</span>[<span style="color:#c10aff">1002</span>];&nbsp;</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#4be6fa">int</span>&nbsp;cnt&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">=</span>&nbsp;<span style="color:#c10aff">1</span>;</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#4be6fa">int</span>&nbsp;a&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">=</span>&nbsp;Integer.<span style="color:#4be6fa">parseInt</span>(st.nextToken());</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#4be6fa">int</span>&nbsp;b&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">=</span>&nbsp;Integer.<span style="color:#4be6fa">parseInt</span>(st.nextToken());</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#999999">//수열&nbsp;만들기</span></div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#ff3399">for</span>&nbsp;(<span style="color:#4be6fa">int</span>&nbsp;i&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">=</span>&nbsp;<span style="color:#c10aff">1</span>;&nbsp;i&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">&lt;</span><span style="color:#0086b3"></span><span style="color:#ff3399">=</span>&nbsp;<span style="color:#c10aff">1000</span>;&nbsp;i<span style="color:#0086b3"></span><span style="color:#ff3399">+</span><span style="color:#0086b3"></span><span style="color:#ff3399">+</span>)&nbsp;{</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#ff3399">for</span>&nbsp;(<span style="color:#4be6fa">int</span>&nbsp;j&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">=</span>&nbsp;<span style="color:#c10aff">0</span>;&nbsp;j&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">&lt;</span>&nbsp;i;&nbsp;j<span style="color:#0086b3"></span><span style="color:#ff3399">+</span><span style="color:#0086b3"></span><span style="color:#ff3399">+</span>)&nbsp;{</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#ff3399">if</span>&nbsp;(cnt&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">=</span><span style="color:#0086b3"></span><span style="color:#ff3399">=</span>&nbsp;<span style="color:#c10aff">1001</span>)&nbsp;<span style="color:#ff3399">break</span>;&nbsp;</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;arr[cnt]&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">=</span>&nbsp;i;</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cnt<span style="color:#0086b3"></span><span style="color:#ff3399">+</span><span style="color:#0086b3"></span><span style="color:#ff3399">+</span>;</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#4be6fa">int</span>&nbsp;sum&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">=</span>&nbsp;<span style="color:#c10aff">0</span>;</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#999999">//수열을&nbsp;만들때,&nbsp;1번째&nbsp;인덱스부터&nbsp;수열을&nbsp;넣어주었으므로&nbsp;a부터&nbsp;b까지의&nbsp;합을&nbsp;구하면&nbsp;됨.</span></div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#ff3399">for</span>&nbsp;(<span style="color:#4be6fa">int</span>&nbsp;i&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">=</span>&nbsp;a;&nbsp;i&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">&lt;</span><span style="color:#0086b3"></span><span style="color:#ff3399">=</span>&nbsp;b;&nbsp;i<span style="color:#0086b3"></span><span style="color:#ff3399">+</span><span style="color:#0086b3"></span><span style="color:#ff3399">+</span>)&nbsp;{</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;sum&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">+</span><span style="color:#0086b3"></span><span style="color:#ff3399">=</span>&nbsp;arr[i];</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bw.write(sum&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">+</span>&nbsp;<span style="color:#ffd500">"\n"</span>);</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bw.close();</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;}</div><div style="padding:0 6px; white-space:pre; line-height:130%">}</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;</div></div><div style="text-align:right;margin-top:-13px;margin-right:5px;font-size:9px;font-style:italic"><a href="http://colorscripter.com/info#e" target="_blank" style="color:#4f4f4ftext-decoration:none">Colored by Color Scripter</a></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#4f4f4f;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div>

이중 루프를 돌리면서 규칙에 맞는 수열을 만들어 주는데, i는 수열에 넣을 숫자이고, j는 i가 들어가는 횟수이고, cnt는 i를 넣을 인덱스를 말한다. 여기서 cnt = 1부터 시작하였으므로 인덱스는 1부터 시작하고 결국 구하는 값은 a와 b의 인덱스 조정없이 바로 구해주면 된다. 