실습
=======

어노테이션
-------
**@Component** 보다 더욱 세분화하기 위하여 **@Controller, @Entity, @Service, @Repository**로 객체지향적으로 분리한다.

- @Controller: 클라이언트로부터 전달되어진 데이터를 가공하기 위한 Controller임을 명시하며 @RequestMapping을 통해 경로설정을 함.
- @Repository: 해당 클래스가 데이터베이스에 접근하는 클래스임을 명시
- @Entity: 일반적인 DBMS
- @Document: MongoDB와 같은 테이블 단위가 아닌 도큐먼트 타입의 디비 지정
- @Service: Repository를 통해 데이터베이스에서 데이터를 가져온 후 **컨트롤러에게 전달해 주는 클래스**임을 명시
- @Autowired: 상황이 타입에 맞는 IoC컨테이너 안에 존재하는 Bean 을 자동으로 주입
- @Transactional: 이 클래스에 트랜잭션 기능이 적용된 프록시 객체가 생서된다. // default: readOnly
   
web.xml
-----

'''xml
  <servlet>
    <servlet-name>mvc</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <init-param>
      <param-name>contextClass</param-name>
      <param-value>org.springframework.web.context.support.AnnotationConfigWebApplicationContext</param-value>
    </init-param>
    <init-param>
      <param-name>contextConfigLocation</param-name>
      <param-value>kr.or.connect.mvcexam.config.WebMvcContextConfiguration</param-value>
    </init-param>
    <load-on-startup>1</load-on-startup>
  </servlet>
  <servlet-mapping>
    <servlet-name>mvc</servlet-name>
    <url-pattern>/</url-pattern>
  </servlet-mapping>
'''

> DispatcherServlet이 오게 되면, WebMvcContextConfiguration을 찾아주세요.
> AnnotationConfigWebApplicationContext을 이용할 것입니다.


'''xml
	<context-param>
		<param-name>contextClass</param-name>
		<param-value>org.springframework.web.context.support.AnnotationConfigWebApplicationContext
		</param-value>
	</context-param>
	<context-param>
		<param-name>contextConfigLocation</param-name>
		<param-value>kr.or.connect.guestbook.config.ApplicationConfig
		</param-value>
	</context-param>
	<listener>
		<listener-class>org.springframework.web.context.ContextLoaderListener
		</listener-class>
	</listener>
'''

> listener는 어떤 특정한 이벤트가 일어났을 때 동작하는 것.
**ContextLoaderListener** : Context가 로딩되는 이벤트가 일어났을 때, Context-param을 참조하게된다. 이 때, param-value에 쓰여있는 클래스 'ApplicationConfig'를 참조하는 것

'''xml
  	<filter>
		<filter-name>encodingFilter</filter-name>
		<filter-class>org.springframework.web.filter.CharacterEncodingFilter
		</filter-class>
		<init-param>
			<param-name>encoding</param-name>
			<param-value>UTF-8</param-value>
		</init-param>
	</filter>
	<filter-mapping>
		<filter-name>encodingFilter</filter-name>
		<url-pattern>/*</url-pattern>
	</filter-mapping>
'''

> filter: 요청이 수행되기 전, 응답이 나가기 전 한 번 씩 걸쳐서 수행을 할 수 있도록 해주는 부분. **url-pattern**: 이 필터를 어디까지 적용할래?
특정한 url지정도 가능함.

  
  


WebMvcConfig설정
-------
WebMvcConfig 클래스는 기본적인 서블릿 설정을 하는 클래스
ViewResolver설정 가능
- **@Configuration**: annotation 으로 이 클래스는 config 클래스라고 명시
- **@EnableWebMvc**: annotation 으로 Spring Web Mvc 설정 클래스라고 명시
- **InternalResourceViewResolver**: 뷰 이름으로부터 JSP나 Tiles 연동을 위한 View 객체를 리턴한다

DBConfig 설정
----
- **TransactionManagementConfigurer**
- **DataSourceTransactionManager**: DataSource를 활용하는 트랜잭션 매니저 등록, dataSource빈을 DataSourceTransactionManager 트랜잭션 매니저의 dataSource속성에 지정

DAO 설정
------
- BeanPropertySqlParameterSource:
> BeanPropertySqlParameterSource는 NamedParameterJdbcTemplate에서 사용되는 파라미터 이름 정보제공 오브젝트의 구현 인터페이스인 **SqlParameterSource**의 구현 클래스
  
  **SqlParameterSource**는 JDBC에서 사용하는 위치 치환자(?) 대신 이름 치환자(이름)을 지원하는 메소드에서 각 이름에 해당하는 값을 제공해주기 위해서 사용된다.

LogDAO
-----
- usingGeneratedKeyColumns: id가 자동으로 증가
- inserAction: insertAction.executeAndReturnKey - insert 문을 내부적으로 생성하고, 자동으로 생성된 id값을 리턴하게 된다. 이 때, 리턴된 값을 사용할 수 있음.

GuestbookDaoSqls
------
- query들은 상수로 관리
- limit이라는 것을 이용하고 있음. mysql query중 limit을 이용하면, 시작 값, 끝날 때 값을 설정해서 특정 부분만 select 할 수 있음.

GuestbookDao
----
- static import로 GuestbookDaoSqls이용 가능

TEST
-----
- JUNIT 사용해서 학습해보기 **
- main method를 따로 모아둔 Junit

테이블 생성
----
<pre><code>
  CREATE TABLE guestbook(
      id bigint(20) unsigned NOT NULL AUTO_INCREMENT,
      name varchar(255) NOT NULL,
      content text,
      regdate datetime,
      PRIMARY KEY(id)
  );

  CREATE TABLE log(
      id bigint(20) unsigned NOT NULL AUTO_INCREMENT,
      ip varchar(255) NOT NULL,
      method varchar(10) NOT NULL,
      regdate datetime,
      PRIMARY KEY(id)
  );
</code></pre>

ServiceLayer
-------
- Bean 자동 등록: @Autowired -> 알아서 생성해서 주입을 시켜줌.

