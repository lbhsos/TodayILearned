Content-Type 이 application/json 요청이 들어오면, DispatcherServlet은 jsonMessageConvert 를 내부적으로 사용해서 해당 Map 객체를 json 으로 변환해서 전송

@ResponseBody와 @RestController 두 가지 차이점을 알아보기 전에 우선 스프링에서 REST하게 데이터가 송수신되는 과정은 다음과 같다.

- 클라이언트에서 웹서비스에 요청을 보냄
- **Handler Mapping**과 그 타입을 찾는 Dispatcher Servlet에 의해 요청이 가로채짐.
- 요청은 **Controller**에 의해 처리되고 응답은 **Dispatcher Servlet**으로 변환되고 Dispatcher Servlet은 다시 **View**로 보냄


@ResponseBody
------
Spring은 반환 값을 변환하여 HTTP Response에 자동으로 쏜다. Controller 클래스의 각 메소드에는 @ResponseBody 어노테이션이 있어야한다.

@RestController
------
Spring 4.0은 @Controller + @ResponseBody를 합쳐놓은 것 이상의 역할을 수행하는 @RestController를 추가함.  
모든 요청 맵핑 메소드에 @ResponseBody를 추가할 필요가 없어짐.

@PathVariable
------
중괄호에 명시된 값을 변수로 받는다.

@RequestBody
-------
반드시 POST형식으로 응답을 받는 구조여야만 한다. 이를테면 JSON 이나 XML같은 데이터를 적절한 messageConverter로 읽을때 사용하거나, POJO형태의 데이터 전체로 받을경우에 사용된다.