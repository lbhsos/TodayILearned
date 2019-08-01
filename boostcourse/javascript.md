자바 스크립트 변수_연산자_타입
=====

자바스크립트는 컴파일 단계가 없다. 자바스크립트의 type(형)은 실행단계에서 타입이 결정된다.


자바스크립트의 버전
------
* 자바스크립트 버전은 ECMAScript(줄여서ES)의 버전에 따라서 결정되고, 이를 자바스크립트 실행 엔진이 반영한다
* ES5, ES6(ES2015) .. 이런식으로 버전을 일컫는다.
* 2018년을 중심으로 ES6를 지원하는 브라우저가 많아서 몇 년간 ES6 문법이 표준으로 쓰이고 있다.
* ES6는 ES5문법을 포함하고 있어 하위호환성 문제가 없다.
다만 feature별로 지원하지 않는 브라우저가 있을 수 있어 조심해야 한다.

변수
------

변수의 종류에는 var, let, const가 있다.
어떤 것을 사용하는가에 따라 영역, 변수의 유효범위가 달라진다.
ES6 이전까지는 var 를 사용해서 변수를 선언할 수 있다.



연산자
----
연산자 우선순위를 표현하기 위해서는 ()를 사용하면 된다. 

연산자-삼항연산자
----
<pre><code>
const data = 11;
const result = (data>10) ? "ok": "fail";
</code></pre>
논리식 ? 참 : 거짓

연산자 - 비교연산자
----
비교는 == 보다는 ===를 사용한다.
==로 인한 다양한 오류 상황이 존재한다.


자바스크립트의 Type
----
타입은 선언이 아닌 실행타임에 결정된다. 함수 안에서의 파라미터나 변수는 실행될 때 그 타입이 결정된다.
정확하게는 타입 체크시 **toString.call** 함수를 이용해서 그 결과를 매칭하곤 하는데, 문자, 숫자와 같은 자바스크립트 기본타입은 **'typeof'**키워드를 사용해서 체크할 수 있다. 배열 타입은 **isArray** 함수가 표준으로 있다.



자바스크립트 함수
======

함수-함수선언
-------
함수는 여러 개의 인자를 받아서, 그 결과를 출력합니다. 파라미터의 갯수와 인자의 갯수가 일치하지 않아도 오류가 나지 않습니다. 
예를 들어서, 파라미터 1개가 정의된 함수를 부를 때, 인자의 개수를 0개만 넣어서 실행하면, 이미 정의된 파라미터는 undefined라는 값을 갖는다.


>ex) 함수 선언문 예시
<pre><code>
function printName(firstname) {
    var myname = "jisu";
    return myname + " " +  firstname;
}
</code></pre>
 

 함수-함수표현식
 -------
 함수는 아래 printName과 같이 표현할 수 있다.
 이렇게 표현하면 함수 선언문과 달리 선언과 호출순서에 따라서 정상적으로 함수가 실행되지 않을 수 있다.

>ex) 
<pre><code>
function test() { 
    console.log(printName()); 
    var printName = function() {
        return 'anonymouse';
    }
}

test();
</code></pre>


함수-표현식과 호이스팅
앞선 코드에서, printName이 "printName이 is not defined"라고 오류가 나오지 않고, function이 아니라고 나온 이유는 printName이 실행되는 순간 'undefined'로 지정됐기 때문이다.
자바스크립트 함수는 실행되기 전에 함수 안에 필요한 변수값들을 미리 모아서 선언한다. --> **HOSTING**
(실제로 코드가 끌어올라가기 보다는 parser 내부가 그렇게 구현된 것)
따라서 아래 코드 역시 함수를 값으로 가지지만 printName도 변수이므로 값이 undefined로 할당된 상태이다.
<pre><code>
printName(); //아직, printName이 undefined으로 할당된 상태다. 
var printName = function(){}
</code></pre>

함수 - 반환값과 undefined
------
<pre><code>
function printName(firstname) {
    var myname = "jisu";
    var result = myname + " " +  firstname;
}
</code></pre>

자바스크립트 함수는 반드시 return 값이 존재하며, 없을 때는 기본 반환값인 'undefined'가 반환됩니다.
자바스크립트는 void 타입이 없습니다.

함수-arguments객체
-----
함수가 실행되면 그 안에는 arguments라는 특별한 지역변수가 자동으로 생성된다. arguments의 타입은 객체이다. 자바스크립트 함수는 선언한 파라미터보다 더 많은 인자를 보낼 수 있다. 이 때, 넘어온 인자를 arguments로 배열의 형태로 하나씩 접근할 수 있다.



자바스크립트 함수 호출 스택
======


함수 호출
-----
함수 호출시, 반환값을 못 받은 경우 이전 호출 함수들이 계속해서 쌓여서 call stack에 쌓이게 된다. 이 때, 연속적으로 호출하면 call stack이 꽉 차벼러셔 더 실행되지 못하고 오류가 발생한다. 따라서 브라우저에서는 대부분 call stack을 쌓게 미리 설정해둔 경우가 많으며 개발 중 **Maximun call stack size exceeded** 오류를 발견하게 될 수 있다.