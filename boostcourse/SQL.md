SQL(Structured Query Language)
====
* SQL은 데이터를 보다 쉽게 검색하고 추가, 삭제, 수정 같은 조직을 할 수 있도록 고안된 컴퓨터 언어
* 관계형 데이터베이스에서 데이터를 조작하고 쿼리하는 표준 수단
* DML(Data Manipulation Language): 데이터를 조작하기 위해 사용. INSERT, UPDATE, DELETE, SELECT 등이 여기에 해당
* DDL(Data Definition Language): 데이터베이스의 스키마를 정의하거나 조작하기 위해 사용. CREATE, DROP, ALTER 등이 여기에 해당
* DCL(Data Control Language): 데이터를 제어하는 언어. 권한을 관리하고, 데이터의 보안, 무결성 등을 정의합니다. GRANT, REVOKE 등이 여기에 해당

Database 생성하기
----
<pre><code>
mysql -uroot -p
</code></pre>
MySQL 관리자 게정인 root로 데이터베이스 관리 시스템에 접속
> 맥 사용자는 암호 없어서 그냥 엔터키

1. create database DB이름;
2. create database connectdb;

Database 사용자 생성과 권한 주기
------
* Database를 생성했다면, 해당 데이터베이스를 사용하는 계정을 생성해야 한다.
* 또한, 해당 계정이 데이터베이스를 이용할 수 있는 권한을 줘야 한다.
* 아래와 같은 명령을 이용해서 사용자 생성과 권한을 줄 수 있다.
* @'%'는 어떤 클라이언트에서든 접근 가능하다, @'localhost'는 해당 컴퓨터에서만 접근 가능하다는 의미.
* flush privileges는 DBMS에게 적용하라
> 반드시 실행

<pre><code>
grant all privileges on db이름.* to 계정이름@'%' identified by ＇암호’;
grant all privileges on db이름.* to 계정이름@'localhost' identified by ＇암호’;
flush privileges;
</code></pre>

사용자 계정이름은 'connectuser', 암호는 'connect123!@#', 해당 사용자가 사용하는 데이터베이스는 'connectdb'로 계정을 생성하려면 다음과 같이 명령을 수행합니다.

<pre><code>
grant all privileges on connectdb.* to connectuser@'%' identified by 'connect123!@#';

grant all privileges on connectdb.* to connectuser@'localhost' identified by 'connect123!@#';

flush privileges;
</code></pre>


생성한 Database에 접속하기
------
mysql -h호스트명 -uDB계정명 -p 데이터베이스이름
  
db이름이 connectdb, db계정이 connectuser, 암호가 connect123!@# 일 경우 콘솔창에서 다음과 같이 입력합니다.  
mysql -h127.0.0.1 -uconnectuser -p connectdb [enter]

MySQL 연결 끊기 
------
quit 혹은 exit

데이터를 저장하는 공간 테이블
-----
* 마이크로소프트의 엑셀을 실행하면 표가 나온다.
* 데이터베이스도 엑셀의 표화 유사한 테이블을 가짐
* 엑셀과 다른점은 데이터베이스를 생성해도 테이블은 존재하지 않는다.
* 테이블을 사용하려면 테이블을 생성하는 SQL을 사용해야 한다.
* 그리고, 테이블에 값을 저장하려면 저장하기 위한 SQL을 사용해야 한다.

SQL 예제
-----
examples.sql download : <https://github.com/connect-boostcamp/boostcourse_fullstack_web/tree/master/part2>

exampls.sql의 폴더에서, 다음과같은 명령어 수행
> mysql -uconnectuser -p connectdb < examples.sql

> mysql -uconnectuser -p connectdb

> show tables.

table 구조를 확인 하기 위한 describe명령
----
> desc EMPLOYEE;

DML
======

SELECT 구문의 기본문형
---
<img width=500 height=500 src="https://cphinf.pstatic.net/mooc/20180131_187/1517374752273Ba8n9_PNG/2_8_2_select__.PNG">

SELECT 구문 컬럼의 합성(Concation)
------
* 문자열 결합함수 concat 사용  
ex) employee 테이블에서 사번과 부서번호를 하나의 칼럼으로 출력
> SELECT concat(empno,'-',deptno) AS '사번-부서번호'  
> FROM employee;

정렬하기
----
<pre><code>
select empno, name, job from employee order by name;
select empno as 사번, name as 이름, job as 직업 from employee order by 이름;
</code></pre>


특정 행 검색
----
예제 : employee 테이블에서 부서번호가 10또는 30인 사원이름과 부서번호를 출력하시오.
<pre><code>
select name, deptno from employee where deptno in (10, 30);
</code></pre>

  
예제 : employee 테이블에서 이름에 'A'가 포함된 사원의 이름(name)과 직업(job)을 출력하시오.

<pre><code>
select name, job from employee where name like '%A%';
</code></pre>

함수 사용
----
<pre><code>
MOD(n,m) % : n을 m으로 나눈 나머지 값을 출력합니다.
FLOOR(x) : x보다 크지 않은 가장 큰 정수를 반환합니다. BIGINT로 자동 변환합니다.
CEILING(x) : x보다 작지 않은 가장 작은 정수를 반환합니다.
ROUND(x) : x에 가장 근접한 정수를 반환합니다.
POW(x,y) POWER(x,y) : x의 y 제곱 승을 반환합니다.
GREATEST(x,y,...) : 가장 큰 값을 반환합니다.
LEAST(x,y,...) : 가장 작은 값을 반환합니다.
CURDATE(),CURRENT_DATE : 오늘 날짜를 YYYY-MM-DD나 YYYYMMDD 형식으로 반환합니다.
CURTIME(), CURRENT_TIME : 현재 시각을 HH:MM:SS나 HHMMSS 형식으로 반환합니다.
NOW(), SYSDATE() , CURRENT_TIMESTAMP : 오늘 현시각을 YYYY-MM-DD HH:MM:SS나 YYYYMMDDHHMMSS 형식으로 반환합니다. 
DATE_FORMAT(date,format) : 입력된 date를 format 형식으로 반환합니다.
PERIOD_DIFF(p1,p2) : YYMM이나 YYYYMM으로 표기되는 p1과 p2의 차이 개월을 반환합니다.
</pre></code>


테이블 생성
-----
<pre><code>
create table 테이블명( 
          필드명1 타입 [NULL | NOT NULL][DEFAULT ][AUTO_INCREMENT], 
          필드명2 타입 [NULL | NOT NULL][DEFAULT ][AUTO_INCREMENT], 
          필드명3 타입 [NULL | NOT NULL][DEFAULT ][AUTO_INCREMENT], 
          ........... 
          PRIMARY KEY(필드명) 
          );
</code></pre>


테이블 수정(컬럼 추가/삭제)
-----
<pre><code>
alter table 테이블명
          add  필드명 타입 [NULL | NOT NULL][DEFAULT ][AUTO_INCREMENT];

alter table 테이블명
         drop  필드명;
</code></pre>

테이블 수정(컬럼 수정)
-----
<pre><code>
alter table  테이블명
     change  필드명  새필드명 타입 [NULL | NOT NULL][DEFAULT ][AUTO_INCREMENT];
</code></pre>

테이블 이름 변경
------
<pre><code>
alter table  테이블명 rename 변경이름
</code></pre>

테이블 삭제
----
<pre><code>
drop table 테이블이름;
</code></pre>