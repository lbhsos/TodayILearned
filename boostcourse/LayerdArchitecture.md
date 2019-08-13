서비스 객체란?
----
비즈니스 로직을 수행하는 메소드를 가지고 있는 객체.
보통 하나의 비즈니스 로직은 하나의 트랜잭션으로 동작한다.

트랜잭션이란?
-----
1. 원자성
2. 일관성
> 트랜잭션의 작업 처리 결과가 항상 일관성이 있어야 함. 트랜잭션 진행 동안 데이터가 변경되더라도 처음에 진행하기 위해 참조한 데이터로 진행되어야 함
3. 독립성
> 어느 하나의 트랜잭션이라도 다른 트랜잭션의 연산을 방해할수 없다. 
4. 지속성
> 트랜잭션이 성공적으로 완료되었을 경우 결과는 영구적으로 반영되어야 한다.

JDBC 프로그래밍에서 트랜잭션 처리 방법
-----
DB에 연결된 후, Connection 객체의 setAutoCommit 메소드에 false를 파라미터로 지정한다.
입력, 수정, 삭제 SQL이 실행을 한 후 모두 성공했을 경우 Connection 이 가지고 있는 commit() 메소드를 호출한다.

@EnableTransactionManagement
------
pring Java Config파일에서 트랜잭션을 활성화 할 때 사용하는 애노테이션.
  
Java Config를 사용하게 되면 PlatformTransactionManager 구현체를 모두 찾아서 그 중에 하나를 매핑해 사용.
  
특정 트랜잭션 메니저를 사용하고자 한다면 TransactionManagementConfigurer를 Java Config파일에서 구현하고 원하는 트랜잭션 메니저를 리턴하도록 한다.

아니면, 특정 트랜잭션 메니저 객체를 생성시 **@Primary 애노테이션**을 지정합니다.

설정의 분리
-----
- Spring 설정 파일을 프리젠테이션 레이어쪽과 나머지를 분리할 수 있다.

- web.xml 파일에서 프리젠테이션 레이어에 대한 스프링 설정은 *DispathcerServlet*이 읽도록 하고, 그 외의 설정은 *ContextLoaderListener*를 통해서 읽도록 합니다.

- *DispatcherServlet*을 경우에 따라서 2개 이상 설정할 수 있는데 이 경우에는 각각의 DispathcerServlet의 *ApplicationContext*가 각각 독립적이기 때문에 각각의 설정 파일에서 생성한 빈을 서로 사용할 수 없습니다.

- 위의 경우와 같이 동시에 필요한 빈은 **ContextLoaderListener**를 사용함으로써 공통으로 사용하게 할 수 있다.

- **ContextLoaderListener**와 **DispatcherServlet**은 각각 ApplicationContext를 생성하는데, ContextLoaderListener가 생성하는 ApplicationContext가 root컨텍스트가 되고 DispatcherServlet이 생성한 인스턴스는 root컨텍스트를 부모로 하는 자식 컨텍스트가 된다.

- 참고로, 자식 컨텍스트들은 root컨텍스트의 설정 빈을 사용할 수 있습니다.

Spring Layered architecture 구조
-----

<img width=500 height=500 src="https://t1.daumcdn.net/cfile/tistory/991CBB505C6BE2AC02?download">
  
1. Presentation Layer
- Spring MVC 객체
- 프론트 컨트롤러(DispatcherServlet), 컨트롤러, 뷰, 모델

2. Service Layer(Business Layer)
- 실제 비즈니스 로직을 수행하는 컴포넌트
- 컨트롤러(presentation layer)에서 요청을 보내면 DAO(data access layer)를 이용
- 보통 하나의 비즈니스 로직은 하나의 트랜젝션으로 동작(ACID 특징 가정)

3. Data Access Layer(Repository Layer)
- DB에 값을 저장하거나 가져오기 위해 JDBC, Mybatis, JPA 등을 사용해 구현 DAO

Spring Layered Architecture 동작 과정 예시
-----
1. Client에서 요청이 들어오면 먼저 Presentation Layer에서 DispatcherServlet이 Handeler Mapping을 통해 Controller에게 Client요청이 무엇인지 알려줌.

2. Controller는 Business Layer에게 Client 요청 처리를 요구
> Business Layer에 넘겨줄 데이터가 있으면 Domain Object에 담음

3. Business Layer는 Presentation Layer와 Interface를 통해서 통신

4. Business Layer는 Client 요청을 적절히 처리한 후 데이터베이스에 데이터를 저장하거나 데이터를 꺼내기 위해 Data Access Layer에 요청

5. Data Access Layer역시 Business Layer와 Interface를 통해서 통신

6. 모든 처리가 끝나면 Controller는 Client 요청이 처리된 데이터와 사용할 View저ㅓㅇ보를 Domain Object에 가져와 ModelAndView에 담음.

7. ModelAndView 객체를 DispatcherServlet에 넘김

8. DispatcherServlet은 ViewResolver를 통해 View를 선택하고 요청이 처리된 데이터 화면 출력