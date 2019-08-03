scope
=====

4가지 Scope
----
* Application: 웹 어플리케이션이 시작되고 종료될 때까지 변수가 유지되는 경우 사용
* Session: 웹 브라우저 별로 변수가 관리되는 경우 사용
* Request: http요청을 WAS가 받아서 웹 브라우저에게 응답할 때까지 변수가 유지되는 경우 사용
* Page: 페이지 내에서 지역변수처럼 사용

<img width=400 height=400 src="https://cphinf.pstatic.net/mooc/20180129_297/1517205425406SvaC6_JPEG/2_5_1_scope_.jpg">

Page Scope
------
* **PageContext 추상 클래스**를 사용
* JSP 페이지에서 *pageContext*라는 내장 객체로 사용
* forward가 될 경우 해당 Page scope에 지정된 변수는 사용할 수 없다.
* 사용방법은 Application scope나 Session scope, request scope과 같다.
* *마치 지역변수처럼 사용된다는 것이 다른 Scope들과 다르다.*
* jsp에서 pageScope에 값을 저장한 후 해당 값을 EL표기법 등에서 사용할 때 사용된다.
* 지역 변수처럼 해당 jsp나 서블릿이 실행되는 동안에만 정보를 유지하고자 할 때 사용된다.


Request Scope
-----
* http 요청을 WAS가 받아서 **웹 브라우저에게 응답할 때까지 변수값을 유지하고자 할 경우** 사용한다.
* *HttpServletRequest* 객체를 사용한다.
* JSP에서는 *request* 내장 변수를 사용한다.
* 서블릿에서는 HttpServletRequest 객체를 사용한다.
* 값을 저장할 때는 request 객체의 *setAttribute()* 메소드를 사용한다.
* 값을 읽어 들일 때는 request 객체의 *getAttribute()* 메소드를 사용한다.
* forward 시 값을 유지하고자 사용한다.
* forward 하기 전에 request객체의 setAttribute()메소드로 값을 설정한 후, 서블릿이나 jsp에게 결과를 전달하여 값을 출력하도록 하였는데 이렇게 포워드 되는 동안 값이 유지되는 것이 Request scope을 이용했다고 한다.


Session Scope
------
* **웹 브라우저별로 변수를 관리**하고자 할 경우 사용
* 웹 브라우저간의 탭 간에는 세션정보가 공유되기 때문에, 각각의 탭에서는 같은 세션정보를 사용할 수 있다.
* *HttpSession* 인터페이스를 구현한 객체를 사용
* JSP에서는 *session* 내장 변수를 사용
* 서블릿에서는 *HttpServletRequest*의 getSession() 메소드를 이용하여 session 객체를 얻는다
* 값을 저장할 때는 session 객체의 *setAttribute()* 메소드를 사용한다.
* 값을 읽어들일 때는 session 객체의 *getAttribute() * 메소드를 사용한다.
* 장바구니처럼 사용자별로 유지가 되어야 할 정보가 있을 때 사용한다.


Application Scope
----
* 웹 어플리케이션이 시작되고 종료될 때까지 변수를 사용할 수 있다.
* *ServletContext* 인터페이스를 구현한 객체를 사용
* jsp 에서는 *application* 내장 객체를 이용
* 서블릿의 경우는 *getServletContext()* 메소드를 이용하여 application 객체를 이용한다.
* 웹 어플리케이션 하나당 하나의 application 객체가 사용된다.
* 값을 저장할 때는 application 객체의 s*etAttribute()* 메소드를 사용
* 값을 읽어 들일 때는 application 객체의 *getAttribute()* 메소드 사용
* **모든 클라이언트가 공통으로 사용해야 할 값들이 있을 때 사용**