웹의 동작(HTTP 프로토콜의 이해)
========

#### 사람과 사람이 전화 통화를 할 때 몇 가지 규약이 필요하듯이, 웹 브라우저와 웹 서버 간에도 서로 통신하기 위한 규약이 필요하다. 이 때 필요한 규약을 HTTP라고 한다.

학습 목표
----
#### 1. HTTP 프로토콜의 작동방식에 대하여 알아본다.
#### 2. HTTP 프로토콜의 요청/응답 데이터 포맷에 대하여 알아본다.

핵심 개념
---
* HTTP
* Request 형식
* Request Method
* Response 형식
* 응답 코드

HTTP(Hypertext Transfer Protocol)이란?
-----
* 팀 버너스리와 그가 속한 팀은 HTML, 웹 브라우저 및 웹 브라우저 관련 기술 및 HTTP를 발명하였다.
* HTTP는 서버와 클라이언트가 인터넷상에서 데이터를 주고받기 위한 프로토콜이다.
* HTTP는 계속 발전하여 HTTP/2까지 버전이 등장한 상태

HTTP 작동 방식
---
* HTTP는 서버/클라이언트 모델을 따른다
* 장점
    - 불특정 다수를 대상으로 하는 서비스에 적합
    - 클라이언트와 서버가 계속 연결된 형태가 아니기 때문에, 클라이언트와 서버 간의 최대 연결 수보다 훨씬 많은 요청과 응답을 처리할 수 있다.
* 단점
    - 연결을 끊어버리기 때문에, 클라이언트의 이전 상황을 알 수 없다.
    - 이러한 특징을 Stateless(무상태)라고 한다.
    - 이러한 특징 때문에 정보를 유지하기 위해 Cookie와 같은 기술이 등장하였다.

URL(Uniform Resource Locator)
---
* 인터넷 상의 자원의 위치
* 특정 웹 서버의 특정 파일에 접근하기 위한 경로 혹은 주소

HTTP(Hypertext Transfer Protocol)
---
* 요청 메서드: GET, POST, PUT, PUSH, OPTIONS 등의 요청방식이 온다.
* 요청 URI: 요청하는 자원의 위치를 명시
* HTTP 프로토콜 버전: 웹 브라우저가 사용하는 프로토콜의 버전이다.
* GET: 정보를 요청하기 위해서 사용한다.(SELECT)
* POST: 정보를 밀어넣기 위해서 사용한다.(INSERT)
* PUT: 정보를 업데이트하기 위해서 사용한다.(UPDATE)
* DELETE: 정보를 삭제하기 위해서 사용한다.(DELETE)
* HEAD: (HTTP)헤더 정보만 요청한다. 해당 자원이 존재하는지 혹은 서버에 문제가 없는지를 확인하기 위해서 시용한다.
* OPTIONS: 웹서버가 지원하는 메서드의 종류를  요청한다.
* TRACE: 클라이언트의 요청을 그대로 반환한다. 


웹 Front-End와 웹 Back-End
===

#### 웹은 프론트엔드(FE)와 백엔드(BE)로 나눠진다. 브라우저를 프론트엔드 또는 클라이언트라고도 합니다. 웹백엔드는 인터넷 사용자에게는 보이지 않는 것입니다.

학습 목표
---
#### 1. 웹프론트엔드에 대한 역할과 기술적 구성
#### 2. 웹백엔드에 대한 역할과 기술적 구성

핵심 개념
---
* HTML
* CSS
* JavaScript
* 클라이언트
* 서버

웹프론트엔드?
---
 사용자에게 웹을 통해 다양한 콘텐츠(문서, 동영상, 사진 등)를 제공한다.
 또한, 사용자의 요청(요구사항)에 반응해서 동작한다.

웹프론트엔드의 역할
---
* 웹콘텐츠를 잘 보여주기 위해 구조를 만들어야 한다.(신문, 책등과 같이) - HTML
* 적절한 배치와 일관된 디자인 등을 제공해야 한다.(보기 좋게) - CSS
* 사용자 요청을 잘 반영해야 한다.(소통하듯이) - Javascript

웹 백엔드?
---
 backend는 정보를 처리하고 저장하며, 요청에 따라 정보를 내려주는 역할을 한다. 가령 쇼핑몰이라면, 상품 정보를 가지고 있고, 주문을 받아서 저장하고, 사용자가 관심있어 하는 상품을 골라주는 역할이 back-End의 역할이다.

백 엔드 개발자가 알아야 할 것들
---
* 프로그래밍 언어(JAVA, Python, PHP, Javascript 등)
* 웹의 동작 원리
* 알고리즘, 자료구조 등 프로그래밍 기반 지식
* 운영체제, 네트워크 등에 대한 이해
* 프레임워크에 대한 이해(예:Spring)
* DBMS에 대한 이해와 사용방법(예: MySQL, Oracle 등)


browser의 동작
====

 HTML 파일이 올 때 브라우저가 어떻게 렌더링 과정을 거쳐서 보이게 되는지 간단히 이해하기.

핵심개념
---
* Web Browser Rendering

Browser의 동작 1.
---
### [How Browser Work] (https://www.html5rocks.com/en/tutorials/internals/howbrowserswork/)
 페이지 오른쪽 클릭 -> 소스보기
 UI > Browser engine: 브라우저 소프트웨어를 동작시켜주는 핵심 엔진 > Rendering Engine 
 networking module: HTTP
 JavaScript interpreter: 자바스크립트 해석기

Main Flow
---
1. Parsing HTML to construct the DOM tree // 트리구조로 지니고 있음
2. Render tree construction
3. Layout of the render tree
4. Painting the render tree

Parsing General
---
#### 2+3-1 을 해석해야한다면, 기본적인 파싱 방법은
1. 2 분리
2. + 연산자
3. 3
4. - 연산자
5. 1
 + 연산자는 앞과 뒤를 합친다. 등 토큰을 기준으로 syntax tree 를 만들고, 그 트리에 따라서 어떤 값이 처리가 일어나게 된다.

 브라우저는 월드와이드웹에서 정보를 검색, 표현하고 탐색하기 위한 소프트웨어이다.

요약
---
1. 서버와 HTTP로 정보를 주고받을 수 있는 네트워크 모듈을 포함한다.
2. 서버에서 받은 문서(HTML, CSS, Javascript)를 해석하고 실행하여 화면에 표현하기 위한 해석기(Parser)들을 가지고 있다.
3. 브라우저마다 서로 다른 엔진을 포함하고 있다.

렌더링 엔진 처리과정
---
<img width="300" src="https://cphinf.pstatic.net/mooc/20171231_32/1514692895834EoHUo_PNG/webkitflow.png">

1. HTML을 해석하여 DOM Tree를 만든다.
2. CSS를 해석해서 CSS Tree(CSS Object Model)을 만든다.
3. 2번 과정에서 Parsing 과정이 필요하며, 토큰 단위로 해석되는 방식을 일반적인 소스코드의 컴파일 과정
4. *DOM Tree*와 *CSS Tree*, 이 두 개는 연관되어 있으므로 **Render Tree**로 다시 조합된다.
5. 이 조합 결과는 화면에 어떻게 배치할지 크기와 위치 정보를 담고 있다.
6. Render Tree 정보를 통해서 화면에 어떤 부분에 어떻게 색칠을 할지 Painting과정을 거친다.


Browser에서의 웹 개발
====

 HTML 요청 이후 브라우저에서 해석되는 웹페이지(HTML) 안의 내용구성과 소스코드를 어떻게 위치시키면 될지 이해한다.

HTML 문서구조
---
1. 크롬부라우저 열고 크롬 개발자 도구 열기
2. 윈도우 (Ctrl + Shift + l)
맥(Option + Command + i)
3. 접속: <http://www.amazon.com>


웹 서버
===

학습 목표
---
1. 웹 서버의 기능
2. 웹 서버의 종류

핵심 개념
---
* Apache
* Nginx
* HTTP
* 클라이언트(Client)
* 서버(Server)

웹 서버란?
---
* 웹 서버는 소프트웨어를 보통 말하지만, 웹 서버 소프트웨어가 동작하는 컴퓨터를 말함.
* 웹 서버의 가장 중요한 기능은 클라이언트가 요청하는 HTML문서나 각종 Resource를 전달하는 것
* 웹 브라우저나 웹 크롤러가 요청하는 리소스는 컴퓨터에 저장된 정적인 데이터이거나 동적인 결과가 될 수 있음.

웹 서버 소프트웨어의 종류
---
* 가장 많이 사용하는 웹 서버는 *Apache, Nginx, Microsoft IIS*
* Apache 웹 서버는 Apache Software Foundation 에서 개발한 웹서버로 오픈소스 소프트웨어(Open-source Software)이며, 거의 대부분 운영체제에서 설치 및 사용을 할 수 있다.
* Nginx는 **차세대 웹서버**로 불리며 더 적은 자원으로 더 빠르게 데이터를 서비스하는 것을 목적으로 만들어진 서버이며 Apache 웹 서버와 마찬가지로 오픈소스 소프트웨어이다.


WAS
===

학습 목표
----
1. WAS가 무엇인지
2. WAS의 종류
3. 웹서버와 WAS의 차이점

핵심 개념 
---
* WAS(Web Application Server)
* Apache Tomcat

클라이언트/서버 구조
----
 클라이언트(Client)는 서비스(Service)를 제공하는 서버(Server)에게 정보를 요청하여 응답 받은 결과를 사용

DBMS(DataBase Management System)
-----
 다수의 사용자가 데이터베이스 내의 데이터에 접근할 수 있도록 해주는 소프트웨어입니다.

미들웨어(MiddleWare)
------
 클라이언트 쪽에 비즈니스 로직이 많은 경우, 클라이언트 관리(배포 등)로 인해 비용이 많이 발생하는 문제가 있다. **비즈니스 로직을 클라이언트와 DBMS사이의 미들웨어 서버에서 동작하도록 함**으로써 클라이언트는 입력과 출력만 담당하도록 한다.

WAS (Web Application Server)
---
WAS는 일종의 미들웨어. 웹 클라이언트(보통 웹 브라우저)의 요청 중 웹 앱이 동작하도록 지원하는 목적을 가짐.

Web Server vs. WAS
---
* WAS도 보통 자체적으로 웹 서버 기능 내장
* 현재는 WAS가 가지고 있는 웹 서버도 정적인 콘텐츠를 처리하는 데 있어서 성능상 큰 차이가 없다.
* 규모가 커질수록 웹 서버와 WAS를 분리
* 자원 이용의 효율성 및 장애 극복, 배포 및 유지보수의 편의성을 위해 웹서버와 WAS를 대체로 분리