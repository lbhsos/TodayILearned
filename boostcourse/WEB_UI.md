window 객체
=======

window는 많은 메서드들이 존재하며, 디폴트의 개념으로 생략이 가능하다.

setTimeout활용
-------
인자로 함수를 받고, 나중에 실행되는 함수를 콜백함수라고도 한다. 자바스크립트는 함수를 인자로 받을 수 있는 특징이 있다.

setTimeout은 비동기(asynchronous)로 실행되어 동기적인 다른 실행이 끝나야 실행된다. 
<pre><code>
function run() {
    console.log("start");
    setTimeout(function() {
        var msg = "hello codesquad";
        console.log(msg);  //이 메시지는 즉시 실행되지 않습니다.
    }, 1000);
    console.log("end");
}

run();
</code></pre>
즉, setTimeout안의 함수(콜백함수)는 run함수의 실행이 끝나고 나서, (정확히는 stack 에 쌓여있는 함수의 실행이 끝나고 나서 실행됨) 실행된다.


DOM과 querySelector
------
브라우저에서는 HTML코드를 **DOM(Document Object Model)**이라는 객체형태의 모델로 저장한다. 그렇게 저장된 정보를 DOM tree라고 한다. 결국 HTML elemet는 Tree형태로 저장된다.

<img width=500 height=500 src="https://cphinf.pstatic.net/mooc/20180126_280/1516956194218XFPk5_PNG/2-2-2_Dom_tree.png">
브라우저에서는 DOM이라는 개념을 통해서, 다양한 DOM API를 제공한다. 즉, DOM Tree를 찾고 조작하는걸 쉽게 도와주는 메서드들이다.

getElementById()
------
ID 정보를 통해서 찾을 수 있다. 

Element.querySelector()
------
DOM을 찾는데 특히 유용한 querySelector메서드이다. CSS 스타일을 결정할 때 사용하던, Selector 문법을 활용해 DOM에 접근할 수 있다.

Q. querySelectorAll() 과 비교해보기!

css selector
------
selector 문법은 querySelector와 querySelectorAll메서드에서 사용할 수 있다.


참고링크: <https://en.wikipedia.org/wiki/Document_Object_Model>


Brower Event, Event object, Event handler
=====


이벤트 등록
------
addEventListener 함수 사용
<pre><code>
var el = document.querySelector(".outside");
el.addEventListener("click", function(){
//do something..
}, false);
</code></pre>

이벤트 객체
-----
브라우저는 이벤트 리스너를 호출할 때, 사용자로부터 어떤 이벤트가 발생했는지에 대한 정보를 담은 이벤트 객체를 생성해서 리스너 함수에 전달한다. 이벤트 리스너 안에서는 이벤트 객체를 활용해서 추가적인 작업을 할 수 있다.
<pre><code>
var el = document.getElementById("outside");
el.addEventListener("click", function(evt){
 console.log(evt.target);
 console.log(evt.target.nodeName);
}, false);
</code></pre>
event.target은 이벤트가 발생한 element를 가리킨다. element도 객체이므로 안에 nodeName이나 classname과 같이 element가 가진 속성을 사용할 수 있다.


Ajax통신의 이해
=====


Ajax (XMLHTTPRequest 통신)
----
누르지도 않은 탭의 컨텐츠까지 초기로딩시점에 모두 불러온다면 초기로딩속도에 영향을 줄 것이다. 따라서 동적으로 필요한 시점에 컨텐츠를 받아와서 표현한다.

Ajax 통신으로는 XML, Plain Text, JSON 등 다양한 포맷의 데이터를 주고받을 수 있지만, 일반적으로 사용이 편리한 JSON포맷으로 데이터를 주고 받습니다


AJAX 실행코드
-----

XMLHttpRequest객체를 생성해서, **open메서드**로 요청을 준비하고, **send메서드**로 서버로 보낸다. 

요청처리가 완료되면(서버에서 응답이 오면) **load**이벤트가 발생하고, **콜백함수가 실행**된다.

콜백함수가 실행될 때는 이미 **ajax함수는 반환하고 콜스택에서 사라진 상태**입니다. 

이는 setTimeout함수의 콜백함수의 실행과 유사하게 동작하는 '비동기'로직 입니다.
참고: <https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/Using_XMLHttpRequest>

