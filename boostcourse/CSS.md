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
