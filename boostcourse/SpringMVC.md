MVC
====

MVC는 Model-View-Controller의 약자이다.
원래는 제록스 연구소에서 일하던 트뤼그베 린즈커그가 처음으로 소개한 개념으로, 데스트톱 어플리케이션용으로 고안되었다.

- Model : 모델은 뷰가 **렌더링하는데 필요한 데이터**이다. 예를 들어 사용자가 요청한 상품 목록이나, 주문 내역이 이에 해당합니다.
- View : 웹 애플리케이션에서 뷰(View)는 실제로 보이는 부분, 모델을 사용해 렌더링을 한다. 뷰는 JSP, JSF, PDF, XML등으로 결과를 표현한다.
- Controller : 컨트롤러는 사용자의 액션에 응답하는 컴포넌트이다. 컨트롤러는 모델을 업데이트하고, 다른 액션을 수행한다.

아키텍처 1
<img width=500 height=300 src="https://cphinf.pstatic.net/mooc/20180219_180/1519003368125BcfqV_PNG/1.png">

  
아키텍처 2
<img width=500 height=300 src="https://cphinf.pstatic.net/mooc/20180219_65/1519003382079lUcI5_PNG/2.png">

Spring MVC 구성요소
======

Spring MVC 기본 동작 흐름
----
<img width=500 height=500 src="https://cphinf.pstatic.net/mooc/20180219_116/1519003779294ejdEx_PNG/1.png">

SpringMVC는 모델 2 아키텍처로 구성되어있다.
Database를 제외한 파란 부분은 Spring MVC가 제공해준다. 개발자가 만들어야 할 부분들은 보라색이며, 녹색 부분(View)은 개발자가 만들어야하는 부분과 Spring MVC 가 제공해주는 부분이 합쳐진 부분이다.
  
요청을 보내면, **Dispatcher Servlet()**클래스가 받는다. Dipatcher Servlet은 컨트롤러와 메서드가 무엇인지 **Handler Mapping**에게 물어본다. 어떤 요청에 어떤 컨트롤러가 동작할지를 xml파일이나 java파일에 어노테이션으로 설정한다. 

이후에, **Handler Adapter** 에게 결정된 컨트롤러와 해당 메서드가 실행되고, 그 결과를 Model에게 Dispatcher Servlet이 받는다. 이 때, view name을 받게 되는데 **View Resolver**를 통해서 view를 출력한다.

DispatcherServlet
-----
* 프론트 컨트롤러 (Front Controller)
* 클라이언트의 모든 요청을 받은 후 이를 처리할 핸들러에게 넘기고 핸들러가 처리한 결과를 받아 사용자에게 응답 결과를 보여준다.
* DispathcerServlet은 여러 컴포넌트를 이용해 작업을 처리한다.

[DispatcherSevlet 내부 동작 흐름]
<img width=500 height=500 src="https://cphinf.pstatic.net/mooc/20180219_281/1519003870301bOehw_PNG/2.png">

  
요청 선처리 작업시 사용된 컴포넌트
-----
**org.springframework.web.servlet.LocaleResolver**

- 지역 정보를 결정해주는 전략 오브젝트이다.
> 지역화: 똑같은 사이트에 들어가도, 사용자마다 웹페이지 언어가 다르게 표시 / 각 사용자의 브라우저의 언어 셋팅에 따라서!
- 디폴트인 *AcceptHeaderLocalResolver*는 HTTP 헤더의 정보를 보고 지역정보를 설정해준다.

**org.springframework.web.servlet.FlashMapManager**

- FlashMap객체를 조회(retrieve) & 저장을 위한 인터페이스
> FlashMap은 스프링에서 파라미터를 간편하게 전달하기 위한 자료구조
- RedirectAttributes의 addFlashAttribute메소드를 이용해서 저장한다.
- 리다이렉트 후 조회를 하면 바로 정보는 삭제된다.

**org.springframework.web.context.request.RequestContextHolder**

- 일반 빈에서 HttpServletRequest, HttpServletResponse, HttpSession 등을 사용할 수 있도록 한다.
- 해당 객체를 일반 빈에서 사용하게 되면, Web에 종속적이 될 수 있다.

**org.springframework.web.multipart.MultipartResolver**

- 멀티파트 파일 업로드를 처리하는 전략

[요청 선처리 작업]
<img width=500 height=500 src="https://cphinf.pstatic.net/mooc/20180219_91/1519003885824QT31y_PNG/3.png">

  
요청 전달시 사용된 컴포넌트
-----
**org.springframework.web.servlet.HandlerMapping**

- HandlerMapping구현체는 **어떤 핸들러가 요청**을 처리할지에 대한 정보를 알고 있다.
- 디폴트로 설정되는 있는 핸들러매핑은 **BeanNameHandlerMapping**과 **DefaultAnnotationHandlerMapping** 2가지가 설정되어 있다.

**org.springframework.web.servlet.HandlerExecutionChain**

- HandlerExecutionChain구현체는 실제로 호출된 핸들러에 대한 참조를 가지고 있다.
- 즉, *무엇이 실행되어야 될지 알고 있는 객체*라고 말할 수 있으며, 핸들러 실행전과 실행후에 수행될 *HandlerInterceptor*도 참조하고 있다.

**org.springframework.web.servlet.HandlerAdapter**

- **실제 핸들러를 실행하는 역할**을 담당한다.
- 핸들러 어댑터는 선택된 핸들러를 실행하는 방법과 응답을 **ModelAndView**로 변화하는 방법에 대해 알고 있다.
- 디폴트로 설정되어 있는 핸들러 어댑터는 *HttpRequestHandlerAdapter, SimpleControllerHandlerAdapter, AnnotationMethodHanlderAdapter 3가지*이다.
- @RequestMapping과 @Controller 애노테이션을 통해 정의되는 컨트롤러의 경우 DefaultAnnotationHandlerMapping에 의해 핸들러가 결정되고, 그에 대응되는 AnnotationMethodHandlerAdapter에 의해 호출이 일어난다.

<img width=500 height=500 src="https://cphinf.pstatic.net/mooc/20180219_20/1519003954110F9wyd_PNG/4.png">
  


요청 처리시 사용된 컴포넌트
-----
**org.springframework.web.servlet.ModelAndView**

- ModelAndView는 Controller의 *처리 결과*를 보여줄 view와 view에서 사용할 값을 전달하는 클래스이다.

**org.springframework.web.servlet.RequestToViewNameTranslator**

- 컨트롤러에서 뷰 이름이나 뷰 오브젝트를 제공해주지 않았을 경우(뷰가 없을 때) URL과 같은 요청정보를 참고해서 자동으로 뷰 이름을 생성해주는 전략 오브젝트이다. 디폴트는 DefaultRequestToViewNameTranslator이다.

<img width=500 height=500 src="https://cphinf.pstatic.net/mooc/20180219_167/1519004040926yL8eC_PNG/5.png">
  


예외 처리시 사용된 컴포넌트
----

**org.springframework.web.servlet.handlerexceptionresolver**

- 기본적으로 DispatcherServlet이 **DefaultHandlerExceptionResolver**를 등록한다.
- HandlerExceptionResolver는 예외가 던져졌을 때 어떤 핸들러를 실행할 것인지에 대한 정보를 제공한다.

<img width=500 height=300 src="https://cphinf.pstatic.net/mooc/20180219_26/1519004078279fGdRP_PNG/6.png">
  

뷰 렌더링 과정시 사용된 컴포넌트
-----
**org.springframework.web.servlet.ViewResolver**

- 컨트롤러가 리턴한 뷰 이름을 참고해서 적절한 뷰 오브젝트를 찾아주는 로직을 가진 전략 오프젝트이다.
- 뷰의 종류에 따라 적절한 뷰 리졸버를 추가로 설정해줄 수 있다.

<img width=500 height=300 src="https://cphinf.pstatic.net/mooc/20180219_66/1519004113425TanBR_PNG/7.png">


