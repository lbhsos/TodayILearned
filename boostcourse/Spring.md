Spring
======

Spring Framework란?
------
* 엔터프라이즈급 어플리케이션을 구축할 수 있는 가벼운 솔루션이자, 원스-스탑-숍(One-Stop-Shop)
* 원하는 부분만 가져다 사용할 수 있도록 **모듈화**가 잘 되어있음
* IoC 컨테이너
* 선언적으로 트랜잭션을 관리할 수 있음
* 완전한 기능을 갖춘 MVC Framework 제공
* AOP 지원
* 스프링은 도메인 논리 코드와 쉽게 분리될 수 있는 구조

프레임 워크 모듀
------
- 스프링 프레임워크는 약 **20개의 모듈**로 구성되어 있음
- 필요한 모듈만 가져다 사용 가능


AOP와 인스트루맨테이션(instrumentation)
-------
- spring-AOP: AOP 얼라이언스(Aliance)와 호환되는 방법으로 AOP를 지원
- spring-aspects: AspectJ와의 통합을 제공
- spring-instrument: **인스트루멘테이션**을 지원하는 클래스와 특정 WAS에서 사용하는 클래스로 더 구현체를 제공. 참고로 BCI(Byte Code Instrumentations)은 런타임이나 로드(Load) 때 클래스와 바이트 코드에 변경을 가하는 방법을 말해줌.


메시징(Messaging)
-------
* spring-messaging: 스프링 프레임워크 4는 메시지 기반 어플리케이션을 작성할 수 있는 Message, MessageChannel, MessageHandler 등을 제공한다. 또한, 해당 모듈에는 메소드에 메시지를 맵핑하기 위한 어노테이션도 포함되어 있으며 Spring MVC 어노테이션과 유사하다.

데이터 액서스(Data Access) / 통합(Integration)
------
- 데이터 액세스/통합 계층은 JDBC, ORM, OXM, JMS 및 트랜잭션 모듈로 구성되어 있다.
- **spring-jdbc**: 자바 JDBC 프로그래밍을 쉽게 할 수 있도록 기능 제공
- **spring-tx**: 선언적 트랜잭션 관리를 할 수 있는 기능 제공
- spring-orm: JPA, JDO 및 Hibernate를 포함한 ORM API 를 위한 통합 레이어 제공
- spring-oxm: JAXB, Castor, XMLBeans, JiBX 및 XStream 과 같은 Object/XML 맵핑을 지원
- spring-jms: 메시지 생성(producing) 및 사용(consumming)을 위한 기능 제공, Spring Framework 4.1부터 spring-messaging 모듈과의 통합을 제공


웹(Web)
-----
- 웹 계층은 *spring-web, spring-webmvc, spring-websocket, spring-webmvc-portlet* 모듈로 구성된다.
- **spring-web**: 멀티 파트 파일 업로드, 서블릿 리스너 등 웹 지향 통합 기능을 제공. *HTTP 클라이언트와 Spring 원격 지원을 위한 웹 관련 부분을 제공*
- **spring-webmvc**: Web-Servlet 모듈이라고도 불리며, Spring MVC 및 REST 웹 서비스 구현을 포함한다.
- spring-websocket: 웹 소켓을 지원한다.
- spring-webmvc-portlet: 포틀릿 환경에서 사용할 MVC 구현을 제공


컨테이너(Container)
------
- 컨테이너는 인스턴스의 생명주기를 관리, 생성된 인스턴스에게 추가적인 기능을 제공.
> 예를 들어, Servlet을 실행해주는 WAS는 Servlet 컨테이너를 가지고 있다고 말합니다. WAS는 웹 브라우저로부터 서블릿 URL에 해당하는 요청을 받으면, 서블릿을 메모리에 올린 후 실행합니다.  
개발자가 서블릿 클래스를 작성했지만, 실제로 메모리에 올리고 실행하는 것은 WAS가 가지고 있는 Servlet 컨테이너입니다.  
Servlet컨테이너는 동일한 서블릿에 해당하는 요청을 받으면, 또 메모리에 올리지 않고 기존에 메모리에 올라간 서블릿을 실행하여 그 결과를 웹 브라우저에게 전달합니다.  
**컨테이너는 보통 인스턴스의 생명주기를 관리하며, 생성된 인스턴스들에게 추가적인 기능을 제공하는 것을 말한다.**
  


IoC(Inversion of Control)
-----
컨테이너가 코드 대신 오브젝트의 제어권을 갖고 있어 **IoC(제어의 역전)**이라 합니다.

> 예를 들어, 서블릿 클래스는 개발자가 만들지만, 그 서블릿의 메소드를 알맞게 호출하는 것은 WAS입니다. (흐름의 제어를 개발자가 아닌 다른 프로그램이 제어하는 것이 IoC)

이렇게 개발자가 만든 어떤 클래스나 메소드를 다른 프로그램이 대신 실행해주는 것을 제어의 역전이라고 합니다.


DI(Dependency Injection)
-----
DI는 의존성 주입이란 뜻, **클래스 사이의 의존 관계를 빈(Bean) 설정 정보를 바탕으로 컨테이너가 자동으로 연결**해주는 것을 말한다.

Spring에서 제공하는 IoC/DI 컨테이너
------
- BeanFactory : IoC/DI에 대한 기본 기능을 가지고 있습니다.
- ApplicationContext : BeanFactory의 모든 기능을 포함하며, 일반적으로 *BeanFactory보다 추천*됩니다. 트랜잭션처리, AOP등에 대한 처리를 할 수 있습니다. BeanPostProcessor, BeanFactoryPostProcessor등을 자동으로 등록하고, 국제화 처리, 어플리케이션 이벤트 등을 처리할 수 습니다.
- BeanPostProcessor : 컨테이너의 기본로직을 오버라이딩하여 인스턴스화 와 의존성 처리 로직 등을 개발자가 원하는 대로 구현 할 수 있도록 합니다.
- BeanFactoryPostProcessor : 설정된 메타 데이터를 커스터마이징 할 수 있습니다.

Java Config를 이용한 설정을 위한 어노테이션
-------
@Configuration
- 스프링 설정 클래스를 선언하는 어노테이션
@Bean
- bean을 정의하는 어노테이션
@ComponentScan
- @Controller, @Service, @Repository, @Component 어노테이션이 붙은 클래스를 찾아 컨테이너에 등록
@Component
- 컴포넌트 스캔의 대상이 되는 애노테ㅣ션 중 하나로써 주로 유틸, 기타 지원 클래스에 붙이는 어노테이션
@Autowired
- 주입 대상이 되는 bean을 컨테이너에 찾아 주입하는 어노테이션

DTO
-----
- DTO란 Data Transfer Object의 약자입니다.
- 계층간 데이터 교환을 위한 자바빈즈입니다.
- 계층이란 컨트롤러 뷰, 비지니스 계층, 퍼시스턴스 계층을 의미합니다.
- 일반적으로 DTO는 로직을 가지고 있지 않고, 순수한 데이터 객체입니다.
- 필드와 getter, setter를 가진다. 추가적으로 toString(), equals(), hashCode()등의 Object 메소드를 오버라이딩 할 수 있습니다.

ConnectionPool
----
- DB연결은 비용이 많이 듭니다.
- 커넥션 풀은 미리 커넥션을 여러 개 맺어 둡니다.
- 커넥션이 필요하면 커넥션 풀에게 빌려서 사용한 후 반납합니다.
- 커넥션을 반납하지 않으면 어떻게 될까요?
> 사용가능한 커넥션이 없어지면, 비용이 많이 들게되므로, 빨리 사용하고 빨리 반납한다.

DataSource
----- 
- DataSource는 커넥션 풀을 관리하는 목적으로 사용되는 객체입니다.  
- DataSource를 이용해 커넥션을 얻어오고 반납하는 등의 작업을 수행합니다.


JdbcTemplate외의 접근방법
-----
- NamedParameterJdbcTemplate:
JdbcTemplate에서 JDBC statement 인자를 ?를 사용하는 대신 파라미터명을 사용하여 작성하는 것을 지원

- SimpleJdbcTemplate:
JdbcTemplate과 NamedParameterJdbcTemplate 합쳐 놓은 템플릿 클래스
이제 JdbcTemplate과 NamedParameterJdbcTemplate에 모든 기능을 제공하기 때문에 삭제 예정될 예정(deprecated)

- SimpleJdbcInsert:
테이블에 쉽게 데이터 insert 기능을 제공

실습
----
BeanPropertyRowmapper: java변수명과 jdbc변수명을 일치시켜줌.