# SQL 이란?
관계형 데이터베이스에서 데이터 정의, 데이터 조작, 데이터 제어를 하기 위해 사용하는 언어

# SQL의 종류
1. DML(Data Manipulation Language)
- 데이터 조회/입력/수정/삭제 등 데이터를 조작하는 SQL: SELECT, INSERT, UPDATE, DELETE 등
- 데이터의 검색 및 출력, 정렬과 조인에 관계됨: WHERE, ORDER BY, GROUP BY, HAVING, UNION 등

2. DDL(Data Definition Language)
- 테이블 및 객체의 구조 생성 및 삭제, 변경과 관계된 명령어: CREATE, DROP, ALTER 등

3. DCL(Data Control Language)
- 권한 제어용, DB 사용자의권한 정의에 사용됨. 주로 DBA 사용. : GRANT, REVOKE

# ANSI SQL ?
: The American National Standards Institute Structured Query Language
|오라클 SQL|ANSI SQL|
|:---|:---|
|select * <br/> from 영업매출 a, 사원 b, 직무코드 c <br/> where a.판매사원ID=b.사원ID and b.직무ID = c.직무ID(+)|select  * <br/>from  영업매출  <br/>**a inner join** 사원 b<br/>on a.판매사원ID = b. 사원ID<br/>**left outer join** 직무코드 c<br/>on b.직무ID = c.직무ID<br/>where 1 = 1|

# 산술식 및 연결 연산자
연결연산자는 컬럼과 컬럼을 연결한 문자를 결과로 표현한다.
```
SELECT 부서 ID || '' || 사원명 AS 부서사원명
      ,급여금액 || '는 월급여 입니다.' AS 월급여설명
      ,(12*급여금액) + 1000 AS 인센포함연봉
FROM 사원;
```
**NULL 값을  포함한 산술식의 결과는 null**

# 주요 문자 함수
|Function|Purpose|
|:----|:----|
|SUBSTR(column\|expr, m[,n])|m과 n 사이에 있는 문자열만 반환(m이 음수이면, 문자열의 끝에서  시작. n을 생략하면, 문자열 끝까지 모두 반환)|
|LENGTH(column\|expr)|표현식에서 문자의 갯수를 반환(LENGTHB는 문자의 바이트수를 반환)|
|LPAD(xolumn\|expr, n, 'str')|n의 자릿수를 가진 문자열 형태로 오른쪽  정렬을 한다. 'str'을 왼쪽에 추가|
|RPAD(xolumn\|expr, n, 'str')|n의 자릿수를 가진 문자열 형태로 왼쪽  정렬을 한다. 'str'을 오른쪽에 추가|

# 주요 숫자 함수
|Function|Purpose|
|:----|:----|
|ROUND(column\|expr, n)|컬럼, 표현식, 또는 값에 대해 소수점 n번째 자리에서 반올림한다. n이 생략되면, 소수점은 없다.|
|TRUNC(column\|expr, n)| 컬럼, 표현식, 또는 값에 대해 소수점 n 번째 자리의 나머지는 버린다.|
|MOD(m,n)|m을 n으로 나눈 나머지를 반환한다.|

|Function 예시|결과 예시|
|:----|:----|
|ROUND(45.923, 2)|45.92|
|ROUND(45.923, 0)|46|
|ROUND(45.923, -1)|50|
|TRUNC(45.923, 2)|45.92|


# NVL  함수
- Null 값을 의미가 부여된 값으로 변환
- 데이터 형식은 일치해야 한다.
- NVL(성과급율, 0)
- NVL(직무ID, 'No Job Yet')

# Case, Decode 조건문활용
- SQL 문 안에 IF - THEN - ELSE 논리 사용
```
SELECT 사원명, 직무ID,
    CASE 직무ID
    WHEN 'J21' THEN 1.10*급여금액
    WHEN 'J22' THEN 1.15*급여금액
    WHEN 'J23' THEN 1.20*급여금액
    ELSE 급여금액 END AS "REVISED_급여금액"
FROM 사원;
```
```
SELECT 사원명, 직무ID
    DECODE(직무ID, 'J21', 1.10*급여금액, 
    'J22', 1.15*급여금액,
    'J23', 1.20*급여금액, 급여금액)
    AS "REVISED_급여금액"
FROM 사원;
```

# 서브쿼리 개념
|서브쿼리|설명|
|----|----|
|인라인뷰|select 문장을 FROM 절에서 테이블처럼 사용하는 쿼리|
|서브쿼리|select 문장을 where 절에서 메인쿼리의 조건으로 사용하는 쿼리<br />EXIST, IN 연산자 사용하는 쿼리|
|스칼라 서브쿼리|select 절에 기술하여 1로우, 1개 컬럼을 반환하는 함수 같은 역할을 하는 쿼리|

# WITH문이란
- select 문장에 구현하기 어려운 inLineView을 with문으로 구현하고 SELECT문에서 테이블처럼 사용
```
WITH with_사원 AS
(SELECt * FROM 사원),
with_부서 AS (SELECT * FROM 부서코드 A),
with_사원부서 AS (
    SELECT A.*, B.부서명
    FROM with_사원 A, with_부서 B
    WHERE A.부서ID = B.부서ID
)
select * from with_사원부서;
```

# 윈도우함수 - ROLLUP
```
SELECT 주문일자, 판매사원ID, SUM(주문수량)
FROM 영업매출
WHERE 상품번호='PRD01'
AND 주문일자 LIKE '201701%'
GROUP BY ROLLUP (주문일자,판매사원ID)
```
GROUP BY와 함께, 소계, 총계를 구함.

# RANK()
- rank() over : 순위를 매기되, 중복된 순위갯수를 모두 순위에 포함. 예를 들면 1, 2, 2, 4 등과 같음
-  dense_rank() over: 순위를 매기되, 순서대로 순위 매김. 예를 들면 1, 2, 2, 3
- row_number(): 중복없이 순서매김. 1,2,3,4

# SUM()
- 누적 합계 가능
- SUM(급여금액) over (order by 급여금액) 누적
