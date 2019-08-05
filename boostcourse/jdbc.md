JDBC(Java Database Connectivity)
======

- 자바를 이용한 데이터베이스 접속과 SQL 문장의 실행, 그리고 실행 결과로 얻어진 데이터의 핸들링을 제공하는 방법과 절차에 관한 규약  
- 자바 프로그램 내에서 SQL문을 실행하기 위한 자바 API  
- SQL과 프로그래밍 언어의 통합 접근 중 한 형태  

JDBC 환경 구성
-----
* JDK 설치
* JDBC 드라이버 설치
- Maven 에 다음과 같은 의존성 추가
'''html
<dependency>   
  <groupId>mysql</groupId>   
       <artifactId>mysql-connector-java</artifactId>
       <version>5.1.45</version>
 </dependency>
'''

* JAVA API reference: <https://docs.oracle.com/javase/8/docs/api/>
* JDBC Tutorial: <https://docs.oracle.com/javase/tutorial/jdbc/basics/index.html>

JDBC를 이용한 프로그래밍 방법
-----
1. import java.sql.*;
2. 드라이버를 로드 한다.
3. Connection 객체를 생성한다.
4. Statement 객체를 생성 및 질의 수행
5. SQL문에 결과물이 있다면 ResultSet 객체를 생성한다.
6. 모든 객체를 닫는다.

JDBC 클래스의 생성 관계
------
<img width=800 height=400 src="https://cphinf.pstatic.net/mooc/20180201_49/1517475141729UGWfv_PNG/2_11_1_JDBC_.PNG">
