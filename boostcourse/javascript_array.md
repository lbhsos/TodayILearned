자바스크립트 배열
====

배열의 선언 
----
<pre><code>
var a = new Array();
var b = []
var c = [4];
c[1000] = 3;
console.log(c.length);
</code></pre>
1. 배열 안에는 모든 타입이 들어갈 수 있다. 
> 배열 안 배열, 배열 안 객체 가능
2. new Array() 또는 '[]'를 사용한다
3. length 속성으로 길이를 쉽게 알 수 있다.
4. 배열에 원소 추가는 index 번호와 함께 추가 가능
5. push 메서드를 통해서 뒤에 순차적 추가 가능


배열의 유용한 메서드들
-----
배열은 순서가 있고, push 와 같은 메소드를 제공하고 있어, 추가/삭제/변경이 용이하다.
- indexOf(): 배열의 원소에 특정 값이 들어있는지 확인
> [1,2,3,4].indexOf(3) // 2
- join(): 배열을 문자열로 합칠 수 있음
> [1,2,3,4].join() // "1,2,3,4"
- concat(): 배열을 합칠 수 있음
> [1,2,3,4].concat(2,3) // [1,2,3,4,2,3]

배열의 여러가지 메서드도 모두 함수이므로 반환 값이 존재한다. 어떤 메서드는 원래 배열의 값을 변경시킨다. 예를 들어서 원래 배열은 그대로 있고 합쳐진 새로운 배열을 반환한다. 따라서, 두 배열의 숫자 값이 일치하더라도 주소 값은 다를 수 있다.


배열 탐색(foreach, map, filter)
-----
<pre><code>
["apple", "tomato"].forEach(function(value){
    console.log(value);
});
</code></pre>

forEach를 사용하면 더는 배열의 길이를 체크하는 for 문을 추가하거나, i++과 같은 증가시켜주는 코드가 필요없다. // 자바스크립트 파서가 처리해줌
filter, map과 같이 함수를 인자로 갖는 메서드 중 하나이다.

map은 새로운 배열을 반환하는 메서드이다
<pre><code>
var newArr = ["apple","tomato"].map(function(value, index) {
   return index + "번째 과일은 " + value + "입니다";
});
console.log(newArr)// 여러분들이 실행해보세요
</code></pre>


객체
----
* key, value 구조의 자료구조
* JavaScript로 데이터를 표현하기 위해서는 Array, Object를 사용
* Object형태는 {}로 표현, 서버와 클라이언트 간 데이터 교환시에도 Object포맷과 비슷한 방법으로 데이터를 보냄


객체의 추가/삭제
-----
<pre><code>
const myFriend = { key : "value", key2 : "value" };
console.log(myFriend);

// 객체 속성 추가
myFriend["name"] = "crong";
console.log(myFriend["name"]);

myFriend.age = 34;
console.log(myFriend.age);

// 객체 속성 삭제
delete myFriend.key;
delete myFriend["key2"];
console.log(myFriend);
</code></pre>


객체의 탐색
-----
<pre><code>
var obj = {"name":"codesquad" , age :22, data: [1,2,3,4,5]};
  
1. for~in 구문 사용
for(value in obj) {
  console.log(obj[value]);
}
  
2. Object.keys() 이용
Object.keys(obj).forEach(function(key) {
	console.log(obj[key]);
});
</code></pre>