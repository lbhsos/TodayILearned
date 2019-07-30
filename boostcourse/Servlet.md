JSP 서블릿(Servlet)이란?
======

자바 웹 어플리케이션의 폴더 구조
------
<img width=500 src="https://cphinf.pstatic.net/mooc/20180124_133/15167752967943AqfC_PNG/1_5_1_____.PNG">

서블릿은 WAS에 동작하는 JAVA 클래스
서블릿은 HttpServlet클래스를 상속받아야 함
예를 들어, 웹 페이지 구성 화면은 JSP로 표현하고, 복잡한 프로그래밍은 서블릿으로 구현한다.

서블릿을 한줄러 정의한다면?
----
웹 프로그래밍에서 클라이언트의 요청을 처리하고 그 결과를 다시 클라이언트에게 전송하는 Servlet 클래스의 구현 규칙을 지킨 자바 프로그래밍 기술

다시 말하면, 서블릿이란 자바를 사용하여 웹을 만들기 위해 필요한 기술이다. 


Servlet 특징
-----
* 클라이언트의 요청에 대해 동적으로 작동하는 웹 어플리케이션 컴포넌트
* html을 사용하여 요청에 응답한다.
* Java Thread를 이용하여 동작한다.
* MVC 패턴에서 Controller로 이용된다.
* HTTP 프로토콜 서비스를 지원하는 javax.servlet.http.HttpServlet 클래스를 상속받는다
* UDP보다 속도가 느리다.
* HTML 변경 시 Servlet을 재컴파일해야하는 단점이 있다.

일반적으로 웹페이지는 정적인 페이지만을 제공한다. 그렇기에 동적인 페이지를 제공하기 위해서는 웹서버는 다른 곳에 도움을 요청하여 동적인 페이지를 작성해야 한다. 동적인 페이지는 간단히 말하면 사용자가 요청한 시점에 페이지를 생성해서 전달해주는 것을 의미한다. 여기서 웹 서버가 동적인 페이지를 제공할 수 있도록 도와주는 어플리케이션이 서블릿이며, 동적인 페이지를 생성하는 어플리케이션이 CGI이다.


Servlet 동작 방식
<img width=400 src="https://t1.daumcdn.net/cfile/tistory/993A7F335A04179D20">

1. 사용자(클라이언트)가 URL 을 클릭하면 HTTP Request를 Servlet Container로 전송한다
2. HTTP Request를 전송받은 Servlet Container는 HttpServletRequest, HttpServletResponse 두 객체를 생성한다.
3. web.xml은 사용자가 요청한 URL을 분석하여 어느 서블릿에 대해 요청을 한 것인지 찾는다.
4. 해당 서블릿에서 service 메소드를 호출한 후 클라이언트의 POST, GET여부에 따라 doGet() 또는 doPost()를 호출한다.
5. doGet() || doPost() 메소드는 동적 페이지를 생성한 후 HttpServletResponse 객체에 응답을 보낸다.
6. 응답이 끝나면 HttpServletRequest, HttpServletResponse 두 객체를 소멸시킨다.


> CGI(Common Gateway Interface)란?
CGI는 특별한 라이브러리나 도구를 의미하는 것이 아니고, 별도로 제작된 **웹서버와 프로그램간의 교환방식**이다. CGI방식은 어떠한 프로그래밍 언어로도 구현이 가능하며, 별도로 만들어 놓은 프로그램에 *HTML의 Get or Post 방법으로 클라이언트의 데이터를 환경변수로 전달*하고, 프로그램의 *표준 출력 결과를 클라이언트에게 전송*하는 것이다. 즉, 자바 어플리케이션 코딩을 하듯 웹 브라우저용 출력 화면을 만드는 방법이다.



서블릿 컨테이너
-----
간단히 설명하면, 서블릿을 관리해주는 컨테이너이다. 즉, 클라이어트의 요청을 받아주고 응답을 할 수 있게 웹서버와 소켓을 만들어 통신하며 대표적인 예로는 톰캣이다.


서블릿 컨테이너의 역할
------
1. 웹서버와 통신 지원
    서블릿 컨테이너는 서블릿과 웹 서버가 손쉽게 통신할 수 있게 해준다. 우리가 일일히 만들어야 할 listen, accept 등을 서블릿 컨테이너가 API로 제공하여 이 과정을 생략할 수있다. 따라서, 개발자가 서블릿에 구현해야 할 비즈니스 로직에만 초점을 둘 수 있다.
2. 서블릿 생명주기 (Life Cycle) 관리
    서블릿 클래스를 로딩하여 인스턴스화하고, 초기화 메소드를 호출하고, 요청이 들어오면 적절한 서블릿 메소드를 호출한다. 또한 서블릿이 생명을 다 한 순간에는 적절하게 Garbage Collection(가비지 컬렉션)을 진행하여 편의를 제공한다
3. 멀티쓰레드 지원 및 관리
    서블릿 컨테이너는 요청이 올 때마다 새로운 자바 쓰레드를 생성하는데, HTTP 서비스 메소드를 실행하고 나면, 쓰레드는 자동으로 죽는다. 
4. 선언적인 보안 관리
    서블릿 컨테이너를 사용하면 개발자는 보안에 관련된 내용을 서블릿 또는 자바 클래스에 구현해 놓지 않아도 된다. 일반적으로 보안관리는 XML 배포 서술자에 기록하므로, 보안에 대해 수정할 일이 생겨도 자바 소스 코드를 수정하여 다시 컴파일 하지 않아도 보안관리가 가능하다.



Servlet 생명주기
-----
<img width=400 src="https://t1.daumcdn.net/cfile/tistory/991870335A04292F0B">

1. 클라이언트 요청 -> 서블릿 메모리 확인 -> init() 메소드 호출하여 적재 -> 실행 중 서블릿이 변경될 경우, 기존 서블릿을 파괴하고 init() 을 통해 새로운 내용을 다시 메모리에 적재
2. init() 호출 -> service() 메소드를 통해 요청에 대한 응답이 doGet() || doPost()로 분기
3. 서블릿 컨테이너는 HttpServletRequest, HttpServletResponse에 의해 request와 response 객체 제공 // Response 는 응답을 해 주는 것, Request는 요청
4. 컨테이너가 서블릿에 종료 요청하면 destroy() 호출 -> 종료시에 처리해야하는 작업들은 destry() 메소드를 오버라이딩하여 구현


[Web] Get과 Post방식의 비교 및 차이
====
사용자가 어떤 홈페이지로 이동하기 위해 URL을 주소창에 입력하고 이동한다. 서버 내부에서는 클라이언트의 요청에 응답하기 위해서 처리가 필요하다. 클라이언트가 서버로 요청을 보내는 방법인 HTTP Method에는 2가지 방식이 있는데 이것이 GET/POST 이다.

1 GET 방식
------

특징
1. URL에 변수(데이터)를 포함시켜 요청
2. 데이터를 Header(헤더)에 포함하여 전송
3. URL에 데이터가 노출되어 보안에 취약
4. 전송하는 길이에 제한
5. 캐싱할 수 있음

GET 방식은 간단한 데이터를 보내도록 설계되어 양에 한계가 있다. 예를 들어 우리가 로그인하려고 id와 pw입력한 후 엔터를 눌렀다고 치면, 
GET www.2stephyun.com/login?id=2step&pw=2step 와 같은 페이지가 있다고 생각해보자. 이렇듯 GET방식을 사용하면 개인정보가 노출되는 문제가 발생한다. GET 방식을 사용하여 데이터를 노출시키는 경우는 개인정보가 포함되지 않는 상황에서 캐싱을 하여 속도를 높이거나 즐겨찾기를 편리하기 위해 사용되는 경우가 많다.

> Cashing 이란?
캐싱이란 한번 접근 후, 또 요청할 시 빠르게 접근하기 위해 레지스터에 데이터를 저장시켜 놓는 것이다. 


2 POST 방식
------

특징
1. URL에 변수를 노출하지 않고 요청
2. data를 body에 포함시킴
3. URL에 데이터가 노출되지 않아서 기본 보안은 되어있다.
4. 전송하는 길이 제한이 없다.
5. 캐싱할 수 없다.

메세지 길이 제한은 없지만 최대 요청을 받는 시간인 Time Out이 존재하므로 클라이언트에서 페이지를 요청하고 기다리는 시간이 존재한다. 실제로 상황에서 POST 방식은 URL에 데이터가 노출되지 않으므로 즐겨찾기나 캐싱이 불가능하지만 쿼리스트링 데이터 뿐 아니라, 라디오 버튼, 텍스트 박스와 같은 객체들의 값도 전송이 가능하다.


버전에 따른 Servlet작성 방법
-------
1. Servlet 3.0 spec 이상에서 사용하는 방법
* web.xml 파일 사용하지 않음
* 자바 어노테이션(annotation) 사용
* 앞에서 실습했던 first web에서 사용

2. Servlet 3.0 spec 미만에서 사용하는 방법
* servlet을 등록할 때 web.xml 파일에 등록



Servlet 3.0 spec 미만시
------
<pre><code>
'''
<?xml version="1.0" encoding="UTF-8"?>
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
xmlns="http://java.sun.com/xml/ns/javaee" 
xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd" 
version="2.5">
    <display-name>exam25</display-name>
    <welcome-file-list>
        <welcome-file>index.html</welcome-file>
        <welcome-file>index.htm</welcome-file>
        <welcome-file>index.jsp</welcome-file>
        <welcome-file>default.html</welcome-file>
        <welcome-file>default.htm</welcome-file>
        <welcome-file>default.jsp</welcome-file>
    </welcome-file-list>
    <servlet>
        <description></description>
        <display-name>TenServlet</display-name>
        <servlet-name>TenServlet</servlet-name>
        <servlet-class>exam.TenServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>TenServlet</servlet-name>
        <url-pattern>/ttt</url-pattern>
    </servlet-mapping>
</web-app>
'''
</code></pre>

의미 정리: 
1. servlet-mapping의 url-pattern 이 /ttt라고 요청이 들어오면, 맵핑에서 찾아내고, 존재하지 않으면 404를 제출
2. servlet-name을 확인하고 servlet 태그 안에서 servlet-name(같은 이름)을 확인한다. -> 짝꿍
3. exam 패키지에서 TenServlet 서블릿을 실행시키는 것
4. 3.0 이상에서는 어노테이션이 대신 해주는 것!