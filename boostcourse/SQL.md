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