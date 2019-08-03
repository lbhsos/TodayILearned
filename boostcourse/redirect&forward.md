Redirect
=====
* 리다이렉트는 HTTP 프로토콜로 정해진 규칙
* 서버는 클라이언트의 요청에 대해 특정 URL로 이동을 요청할 수 있다. => 리다이렉트
* 서버는 클라이언트에게 HTTP 상태코드 302로 응답하는데 이 때, **헤더 내 Location 값에 이동할 URL을 추가**한다. 클라이언트는 리다이렉션 응답을 받게 되면 헤더(Location)에 포함된 URL로 재요청을 보내게 된다. 이 때 브라우저의 주소창은 새 URL로 바뀐다.
* 클라이언트는 서버로부터 받은 상태 값이 302이면 Location 헤더 값으로 재요청을 보내게 된다. 이 때, 브라우저의 주소창은 전송받은 URL로 바뀐다.
* 서블릿이나 JSP는 리다이렉트하기 위해 *HttpServletResponse 클래스의 sendRedirect()*메소드를 사용한다.


브라우저에서 리다이렉트 확인
------
* 크롬에서 우측버튼을 누르고 검사를 선택한 후, Network 탭 선택
* redirect01.jsp를 실행하면 서버로부터 응답코드로 **302**를 받는 것을 알 수 있다.
<img width=500 height=500 src="https://cphinf.pstatic.net/mooc/20180127_5/1517046342330PRbSX_PNG/2_4_1_redirect__.PNG">


Forward
=====
WAS의 서블릿이나 JSP가 요청을 받은 후 그 요청을 처리하다가, 추가적인 처리를 같은 웹 어플리케이션안에 포함된 다른 서블릿이나 JSP에게 위임하는 경우가 있다.
이렇게 위임하는 것을 포워드라고한다.


forward란?
------

<img width=500 height=300 src="https://cphinf.pstatic.net/mooc/20180129_279/1517202070933x0x42_PNG/2_4_2_forward.png">

1. 웹 브라우저에서 Servlet1에게 요청을 보냄
2. Servlet1은 요청을 처리한 후, 그 결과를 **HttpServletRequest**에 저장
3. Servlet1은 결과가 저장된 HttpServletRequest와 응답을 위한 HttpServletResponse를 같은 웹 어플리케이션 안에 있는 Servlet2에게 전송(forward)
4. Servlet2는 Servlet1으로부터 받은 HttpServletRequest와 HttpServletResponse를 이용하여 요청을 처리한 후 웹 브라우저에게 결과 전송


> 서블릿은 프로그램 로직을 개발하기에 편라히자만, HTML태그를 출력하기에는 불편하다. JSP는 프로그램 로직을 개발하기에는 좀 불편하지만, HTML태그를 출력하기엔 편리하다. 


Servlet & JSP 연동
=====

* 서블릿은 프로그램 로직이 수행되기 유리하다. IDE 등에서 자원을 좀 더 잘해준다.
* JSP는 결과를 출력하기에 Servlet보다 유리하다. 필요한 html문을 그냥 입력하면 됨.
* **프로그램 로직 수행은 Servlet**에서, **결과 출력은 JSP에서 하는 것**이 유리하다.
* Servlet과 JSP의 장단점을 해결하기 위해서 Servlet에서 프로그램 로직이 수행되고, 그 결과를 JSP에게 포워딩하는 방법이 사용되게 되었다. 이를 Servlet과 JSP연동이라고 한다.

<img width=500 height=300 src="https://cphinf.pstatic.net/mooc/20180129_201/1517203743283AcQbB_PNG/2_4_3_servlet_jsp.PNG">
