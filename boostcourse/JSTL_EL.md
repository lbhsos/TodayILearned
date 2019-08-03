EL(Expression Language)
======

jsp에서 표현식을 이용해 값을 출력할 때 변수의 값이 null이면 화면에 null이 출력되었다. 이를 방지하기 위해서 불편한 과정을 거쳐야 하는데, EL을 사용하면 좀 더 편리하게 변수를 JSP에서 사용할 수 있다.

표현 언어란?
-----
표현 언어는 값을 표현하는데 사용되는 스크립트 언어로서 JSP의 기본 문법을 보완하는 역할을 한다.

표현 언어가 제공하는 기능
-----
* JSP의 스코프(scope)에 맞는 속성 사용
* 집합 객체에 대한 접근 방법 제공
* 수치 연산, 관계 연산, 논리 연산자 제공
* 자바 클래스 메소드 호출 기능 제공
* 표현 언어만의 기본 객체 제공

표현 언어의 표현 방법
-----
${expr(표현언어가 정의한 문법에 따라 값을 표현하는 식)}

표현 언어는 JSP의 스크립트 요소(스크립트릿, 표현식, 선언부)를 제외한 나머지 부분에서 사용될 수 있으며, 표현식을 통해서 표현식보다 편리하게 값을 출력할 수 있다.

표현 언어의 기본 객체
-----
<img width=500 height=500 src="https://cphinf.pstatic.net/mooc/20180130_153/1517281495386qOuqH_PNG/2_6_1__.PNG">

표현 언어의 데이터 타입
-----
* 불리언 타입
* 정수타입 - 0 ~ 9로 이루어진 정수 값 음수의 경우 '-'가 붙음
* 실수타입 - 0 ~ 9로 이루어져있으며, 소수점('.') 사용 가능, 3.24e3과 같이 지수형으로 표현 가능
* 문자열 타입 - 따옴표('또는")로 둘러싼 문자열. 만약 작은 따옴표(')를 사용해서 표현할 경우 값에 포함된 작은 따옴표는 ₩'와 같이 ₩ 기호와 함께 사용
* ₩ 기호 자체는 ₩₩로 표시
* 널타입 - null

객체 접근 규칙
-----
<pre><code>${<표현1>.<표현2>}</code></pre>
* 표현 1이나 표현 2가 null이면 null을 반환한다.
* 표현1이 **Map**일 경우 표현2를 **key**로한 값을 반환한다.
* 표현1이 **List나 배열**이면 표현2가 정수일 경우 해당 정수 번째 **index**에 해당하는 값을 반환한다.
> 만약 정수가 아닐 경우에는 오류가 발생한다.
* 표현1이 객체일 경우는 표현2에 해당하는 getter메소드에 해당하는 메소드를 호출한 결과를 반환한다.

표현 언어의 수치 연산자
----
* + : 덧셈
* - : 뺄셈
* * : 곱셈
* / 또는 div : 나눗셈
* % 또는 mod : 나머지
* 숫자가 아닌 객체와 수치 연산자를 사용할 경우 객체를 숫자 값으로 변환 후 연산자를 수행 : ${"10"+1} → ${10+1}
* 숫자로 변환할 수 없는 객체와 수치 연산자를 함께 사용하면 에러를 발생 : ${"열"+1} → **에러**
* 수치 연산자에서 사용되는 객체가 null이면 0으로 처리 : **${null + 1} → ${0+1}**


비교 연산자
----
* == 또는 eq
* != 또는 ne
* < 또는 lt
* > 또는 gt
* <= 또는 le
* >= 또는 ge
* 문자열 비교: ${str == '값'} str.compareTo("값") == 0 과 동일

논리 연산자
-----
* && 또는 and
* || 또는 or
* ! 또는 not

표현 언어 비활성화: JSP에 명시하기
<pre><code><%@ page isELIgnored = "true" %></code></pre>


JSTL(JSP Standard Tag Library)
=====
JSTL은 JSP페이지에서 조건문 처리, 반복문 처리 등을 html tag 형태로 작성할 수 있게 도와준다.

JSTL을 사용하려면?
-----
<http://tomcat.apache.org/download-taglibs.cgi>
위의 사이트에서 3가지 jar 파일 다운로드 후 WEB-INF/lib/ 폴더에 복사한다.

<img width=600 height=300 src="https://cphinf.pstatic.net/mooc/20180130_248/1517289861733CmzUv_PNG/2_6_2_jstl_.PNG">

JSTL이 제공하는 태그의 종류
-----
<img width=500 height=500 src="https://cphinf.pstatic.net/mooc/20180130_273/1517290494334HrB7S_PNG/2_6_2_jstl___.PNG">

코어 태그
----
<img width=500 height=500 src="https://cphinf.pstatic.net/mooc/20180130_226/1517290578353rKRbE_PNG/2_6_2_jstl_.PNG">

코어 태그: 변수 지원 태그 - set, remove
----
<h3>변수 설정: 지정한 영역에 변수를 생성한다.</h3>
[문법]

<c:set var="varName" scope="session" value="someValue" />  
<c:set var="varName" scope="request" some Value>  
</c:set>  



* var: EL에서 사용될 변수명
* scope: 변수값이 저장될 영역(page, request, session, application)
* value: 변수값


<h3>변수 제거</h3>
[문법]
<pre><code>
'''html
<c:remove var="varName" scope="request">
'''
</code></pre>

코어태그: 변수지원태그 - 프로퍼티, 맵의 처리
------
[문법]
<pre><code>
'''html
<c:set target="${some}" property="propertyName" value="anyValue" />
some 객체가 자바빈일 경우: some.setPropertyName(anyValue)
some 객체가 맵(map)일 경우: some.put(propertyName, anyValue);
'''
</code></pre>

* target - <c:set>으로 지정한 변수 객체
* property - 프로퍼티 이름
* value - 새로 지정할 프로퍼티 값


코어태그: 흐름제어 태그
-----
[문법]
<pre><code>
<c:if test="조건">
...
...
</c:if>
</code></pre>

코어 태그: 흐름제어 태그-choose
----
<pre><code>
<c:choose>
    <c:when test="조건1">
    </c:when>
    <c:otherwise>
    </c:otherwise>
</c:choose>
</code></pre>


코어 태그: 흐름제어 태그-forEach
-------
[문법]
<pre><code>
<c:forEach var="변수" items="아이템" [begin="시작번호"] [end="끝번호"]>
...
${변수}
...
</c:forEach>
</code></pre>

* var - EL에서 사용될 변수명
* items - 배열, List, Iterator, Enumeration, Map 등의 Collection
* begin - items에 지정한 목록에서 값을 읽어올 인덱스의 시작값
* end - item에 지정한 목록에서 값을 읽어올 인덱스의 끝값

코어 태그: 흐름제어 태그 - import
-----
[문법]
<pre><code>
<c:import url="URL" charEncoding="캐릭터인코딩" var="변수명" scope="범위">
<c:param name="파라미터이름" value="파라미터값" />
</c:import>
</code></pre>

* url: 결과를 읽어올 URL
* charEncoding: 읽어온 결과를 저장할 때 사용할 캐릭터 인코딩
* var: 읽어온 결과를 저장할 변수명
* scope: 변수를 저장할 영역
* <c:param> 태그는 url 속성에 지정한 사이트에 연결할 때 전송할 파라미터를 입력한다.

[예제]
<pre><code>
<c:import url="http://media.daum.net/"
            charEncoding="euc-kr"
            var = "daumNews"
            scope="request">
    <c:param name="_top_G" value="news" />
</c:import>
</code></pre>


코어 태그: 흐름제어태그 - redirect
-----
[문법]
<pre><code>
<c:redirect url="리다이렉트할 URL>
    <c:param name="파라미터이름" value="파라미터값" />
</c:redirect>
</code></pre>
* url -  리다이렉트 URL
* <c:param>은 리다이렉트할 페이지에 전달할 파라미터 지정


코어 태그: 기타태그 - out
-------
[문법]
<pre><code>
<c:out value="value" escapeXml="{true|false}" default="defaultValue" />
</code></pre>

* value: JSPWriter에 출력할 값을 나타냄. 일반적으로 value 속성의 값은 String과 같은 문자열이다. 만약 value 값이 java.io.Reader의 한 종류라면 out 태그는 Reader로부터 데이터를 읽어와 JspWriter에 값을 출력
* escapeXml: 이 속성의 값이 true일 경우 아래 표와 같이 문자를 변경한다. 생략할 수 있으며, 생략할 경우 기본값은 true다.
* default: value 속성에서 지정한 값이 존재하지 않을 때 사용될 값 지정
[표] escapeXml 속성이 true일 경우 반환되는 문자

| 문자 | 변환된 형태 |
| --- | :---:|
| `<` | &lt; |
| `>` | &gt; |
| `&` | &amp; |
| `'` | &#039; |
| `"` | &#034; |


