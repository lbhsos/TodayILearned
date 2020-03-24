# Neo4j로 CSV 데이터 가져오기

[가이드](https://neo4j.com/developer/guide-import-csv/)

## CSV 파일 가져오는 방법
-  LOAD CSV : Cypher 명령으로 중소규모의 데이터 세트(최대 1천만 레코드)를 처리
- neo4j-admin : 대량 가져오기 도구로 큰 데이터 세트를 직접 로드 할 때 유용한 명령 줄 도구
- Kettle import tool : 데이터 프로세스 플로우를 실행하고 맵핑하는데 유용하며, 큰 데이터에도 적합. 개발자가 이 툴을 사용할 수 있으면 매우 좋은 툴임.

### LOAD CSV
<pre><code>
- import 바로 밑에 위치한 경우
LOAD CSV FROM "file:///data.csv"

- import 내 하위 디렉터리 존재
LOAD CSV FROM "file:///northwind/customers.csv"

- URL 을 통해 가져오는 경우
LOAD CSV FROM "https://~"
LOAD CSV WITH HEADERS FROM "https://~"
</code></pre>

- Neo4j 는 null값을 저장하지 않음 --> CSV 파일의 Null 혹은 빈 필드는 생략하거나 기본값으로 바꿀 수 있음 
<pre><code>
LOAD CSV WITH HEADERS FROM 'file:///data.csv' AS row
WITH row WHERE row.Company IS N
OT NULL
MERGE (c:Company { companyId:row.Id})

//set default for null values
LOAD CSV WITH HEADERS FROM 'file:///data.csv' AS row
MERGE (c:Company {companyId: row.Id, hqLocation: coalesce(row.Location, "Unknown")})

//change empty strings to null values (not stored)
LOAD CSV WITH HEADERS FROM 'file:///data.csv' AS row
MERGE (c:Company {companyId: row.Id})
SET c.emailAddress = CASE trim(row.Email) WHEN "" THEN null ELSE row.Email END
</code></pre>