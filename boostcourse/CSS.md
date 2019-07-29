CSS 선언
====

핵심 개념
---
* inline
* internal
* external


CSS의 구성
----
<pre><code>
selector(선택자){
    property: value;
}</code></pre>


style을 HTML 페이지에 적용하는 법 3가지 
##### 1. inline
HTML 태그 안에다가 적용한다.
다른 CSS파일에 적용한 거솝다 가장 먼저 적용

<pre><code>
[예시]
<p style = "border;1px solid gray;color;red;font-size:2em;">
</code></pre>

##### 2. internal
style 태그로 지정
구조와 스타일이 섞이게 되므로 유지보수가 어렵다.
별도의 CSS 파일을 관리하지 않아도 되며 서버에 CSS 파일을 부르기 위해 별도의 브라우저가 요청을 보낼 필요가 없다.
<pre><code>
<head>
<style>
p  {
  font-size : 2em;
  border:1px solid gray;
  color: red;
}
</style>
</head>
</code></pre>

##### 3. external
외부파일(.css)로 지정하는 방식
CSS 코드가 아주 짧지 않다면 가급적 이 방법으로 구현하는 것이 가장 좋다. 현업에서는 여러개의 CSS 파일로 분리하고 이를 합쳐서 서비스에서 사용하기도 한다. internal 코드와 같은 css 코드를 구현하고, style.css와 같은 별도 파일로 만든다.



CSS의 상속
======
상위에서 적용한 스타일은 하위에도 반영이 된다. 그러나 box-model 이라고 불리는 속성들(width, height, margin, padding, border)과 같이 크기와 배치 관련 속성은 하위 에리먼트로 상속되지 않는다. 


우선순위 결정
-----
우선순위 : 
* inline > internal = external
* id > class > element
> id 선언은 #id, class 선언은 .class, 


선언방식에 따른 차이
-----
같은 선택자라면 나중에 선언한 것이 반영된다.
선택자의 표현이 구체적인 것이 있다면 먼저 적용된다.
* body > span (O)
* span(X)

CSS 실습 링크: <https://codepen.io/>
선택자 우선순위 참고 링크: <https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity>



CSS Selector
======
특정 엘리먼트에 스타일을 적용하기 위해서는 해당 엘리먼트를 잘 찾아야 한다. 특정 엘리먼트뿐 아니라 여러 개의 엘리먼트일 수도 있다.


CSS Selector 의 다양한 활용
----
* id, class 요소 선택자와 함께 활용
<pre><code>
#myid {color: red}
div.myclassname{ color: red }
</code></pre>

* 그룹 선택 (여러 개 셀렉터에 같은 style을 적용해야 한다면)
<pre><code>
h1, span, div{color: red}
h1, span, div#id{color:red}
h1.span, div.classname{color: red}
</code></pre>

* 요소 선택(공백): 자손 요소
* 아래는 span tag 2 만 red 색상이 적용된다.
<pre><code>
<div id="jisu">
  <div>
    <span> span tag </span>
  </div>
  <span> span tag 2 </span>
</div>
</code></pre>

* 자식 선택 ('>') : 자식은 바로 하위엘리먼트를 가리킨다.
* n번째 자식요소를 선택합니다. (nth-child)
* 첫 번째 단락에 red 색상 적용
<pre><code>
#jisu > span { color : red }
#jisu > p:nth-child(2) { color : red }
<div id="jisu">
  <h2>단락 선택</h2>
  <p>첫번째 단락입니다</p>
  <p>두번째 단락입니다</p>
  <p>세번째 단락입니다</p>
  <p>네번째 단락입니다</p>
</div>
</code></pre>



CSS 기본 Style 변경하기
======

font 색상 변경
-----
* color: red;
* color: rgba(255,0,0,0.5);
* color: #ff0000; //16진수 표기법

font 사이즈 변경
-----
* font-size: 16px;
* font-size: 1em;

배경색
------
* background-color: #ff0;
* background-image, position, repeat 등 속성이 있음
* background: #0000ff url(".../gif") no-repeat center top;// 한 줄로 정의 가능


글씨체/글꼴
-----
* font-family:"Gulim";
* font-family: monospace;




Element 가 배치되는 방법
=====

엘리먼트를 화면에 배치하는 것을 layout 또는 Rendering 과정이라고 한다.


## 1. 엘리먼트가 배치되는 방식_ display:block
display 속성이 block 이거나 inline-block인 경우 그 엘리먼트는 벽돌을 쌓든 블록을 가지고 쌓입니다.

## 2. 엘리먼트가 배치되는 방식_ display:inline
display 속성이 inline인 경우는 우측으로, 그리고 아래쪽으로 빈자리를 차지하며 흐릅니다. 높이와 넓이를 지정해도 반영되지 않는다.

## 3. 엘리먼트가 배치되는 방식_ position: static, relative, absolute
position 속성은 기본 static
1. absolute 는 기준점에 따라 특별한 위치
- top/left /right / bottom
2. relative 는 원래 자신이 위치해야 할 곳을 기준으로 이동
- top / left /right / bottom
3. fixed는 viewport(전체화면) 좌측, 맨 위를 기준

* margin: 본인과 엘리먼트와의 간격
* float: float 속성으로 원래 flow 에서 벗어날 수 있고 둥둥 떠다닐 수 있다. (float가 자리를 차지하지 않고 떠있다고 생각해서) 
* overflow 속성을 줬을 때는 float을 인식
* box-model: box의 크기와 간격에 관한 속성으로 배치 추가 결정.
* 엘리먼트 크기: block 엘리먼트의 크기는 기본적으로 부모의 크기. width=100%는 부모의 크기만큼
* box-sizing 과 padding: padding속성을 늘리면 엘리먼트의 크기가 달라짐. box-sizing속성으로 **border-box**로 설정한 후, 엘리먼트의 크기를 고정하며 padding 값만 늘릴 수 있음.

Layout 구현방법
-------
전체 레이아웃은 float을 잘 사용해서 2단, 3단 컬럼 배치 구현
특별 위치를 위해서는 position absolute사용, 기준점을 relative로 설정
네비게이션 같은 엘리먼트는 block 엘리먼트를 inline-block으로 변경해서 가로로 배치
엘리먼트 안의 텍스트의 간격과 다른 엘리먼트간의 간격은 padding 과 margin 속성 이용


Debugging
-------
Chrome->Elements탭 Opt+Cmd+I = 개발자도구
