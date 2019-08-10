Web 애니메이션
=====

웹 UI 애니메이션은 자바스크립트로도 가능하지만, 규칙적이고 단순한 방식은 CSS3의 transform속성과 transition 을 사용해서 대부분 구현할 수 있다.

FPS(Frame per second)
-----
FPS는 1초당 화면에 표현할 수 있는 정지화면 수이다.
매끄러운 애니메이션은 보통 60fps이다.

Javscript 애니메이션
-----
* setInterval
* setTimeout
* requestAnimationframe
* Animations API

setInterval()
------
주어진 시간에 따라 함수 실행이 가능하다.

requestAnimationFrame
-----
setTimeout은 animation을 위한 최적화된 기능이라 보기 어렵다.
animation 주기를 16.6 미만으로 하는 경우 불필요한 frame 생성이 되는 등의 문제가 생긴다.
requestAnimationFrame함수를 통해서 원하는 함수를 인자로 넣어주면, 브라우저는 인자로 받은 비동기 함수가 실행될 가장 적절한 타이밍에 실행시켜준다.

CSS 기법으로 애니메이션 구현
-----
transition을 이용한 방법.
이 방법은 JavaScript로 구현하는 것보다 더 빠르다
참조 링크: [여기] (https://thoughtbot.com/blog/transitions-and-transforms)


더 빠른 css3 애니메이션 관련 속성 링크: <https://d2.naver.com/helloworld/2061385>

> 하드웨어 가속이란?
HTML 소스가 로딩되고 파싱되면 브라우저는 태그를 DOM 트리로 구성한다. DOM 트리는 화면에 표현되는 요소와 화면에 표현되지 않는 요소로 이루어져 있다. 예를 들어 head나 script는 화면에 표현되지 않는 DOM 트리 요소이다.

브라우저는 화면에 표현되는 요소를 **RenderObject 트리**로 구성한다. RenderObject 트리의 노드는 **RenderLayer**에 대응된다.
  
RenderLayer 가운데 실제 화면에 출력돼야 하는 노드는 다시 **GraphicsLayer**를 생성한다. 최상위(root)노드나 <canvas>, <video> 등이 **GraphicsLayer**를 생성하는 RenderLayer이다.

하드웨어 가속은 GraphicsLayer 단위로 *렌더링된 이미지를 GPU를 이용해 한 장의 이미지로 합성(composition)해서 화면에 출력*하는 기술이다.

* DOM 트리: HTML 웹 페이지를 파싱한 트리, HTML 문서의 각 요소를 쉽게 처리(추가, 삭제 등)하기 위하여 *브라우저의 엔진이 사용하는 트리*다.
* RenderObject 트리: DOM 트리로부터 만들어지는 트리, DOM 트리의 노드 가운데 *실제 화면에 표현되는 노드*만으로 구성된 트리다.
* RenderLayer: 브라우저의 엔진이 하드웨어 가속 등을 처리하기 위해 사용하는 **논리적인 레이어**로, 각 RenderObject의 속성에 따라 RenderLayer에 할당된다.
* GraphicsLayer: 하드웨어 가속 처리를 위한 *물리적인 레이어*로, 레이어별 RenderObject를 GraphicsLayer 단위로 렌더링한 뒤 최종적으로 GPU를 통해 합성된다.