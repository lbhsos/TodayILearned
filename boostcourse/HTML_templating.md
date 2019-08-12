HTML Templating 
======

HTML Templating 작업이란?
----
반복적인 HTML 부븐을 template로 만들어두고, 서버에서 온 데이터(json)을 결합해서, 화면에 추가하는 작업이다.

<img width=500 height=300 src="https://cphinf.pstatic.net/mooc/20180207_165/1517990489362QgF8S_PNG/3-5-4-2_about_templating.png">

결합과정 해결하기
-----
<pre><code>
var data = {  title : "hello",
              content : "lorem dkfief",
              price : 2000
           };
var html = "<li><h4>{title}</h4><p>{content}</p><div>{price}</div></li>";

html.replace("{title}", data.title)
    .replace("{content}", data.content)
    .replace("{price}", data.price)
</code></pre>

HTML Template 보관
------
아래와 같은 html 문자열을 어딘가 보관해야 한다.
javascript 코드 안에서 이런 정적인 데이터를 보관하는 건 좋지 않다.
<pre><code>
var html = "<li><h4>{title}</h4><p>{content}</p><div>{price}</div></li>";
</code></pre>

* 서버에서 file로 보관하고 Ajax로 요청해서 받아온다.
* HTML코드 안에 숨겨둔다

간단한 것이라면 HTML안에 숨겨 둘 수 있다. 
숨겨야 할 데이터가 많다면 별도의 파일로 분리해서 Ajax로 가져오는 방법도 좋다.

Templating
-------
HTML 중 script 태그는 type이 javascript가 아니라면 렌더링하지 않고 무시한다.
<pre><code>
'''javascript
<script id="template-list-item" type="text/template">
  <li>
      <h4>{title}</h4><p>{content}</p><div>{price}</div>
  </li>
</script>
'''
</code></pre>

이를 이용하면 아래와 같이 간단히 가져올 수 있다.
<pre><code>
var html = document.querySelector("template-list-item");
</code></pre>