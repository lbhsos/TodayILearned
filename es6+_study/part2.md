## 기존과 달라진 es6에서의 리스트 순회
- for i++
- for of

<pre><code>

[기존 es 5]

const list = [1,2,3];
for (var i = 0; i < list.length; i++){
    log(list[i]);
}

const str = 'abc';
for (var i = 0; i < str.length; i++){
    log(str[i]);
}

[es6] -- 보다 선언적으로 변경
for (const a of list){
    log(a);
}

for(const a of str){
    log(a);
}
</code></pre>

### Array를 통해 알아보기
<pre><code>
const arr = [1,2,3];
for (const a of arr) log(a);
</code></pre>
Array 같은 경우는 key로 접근하여 조회 가능.

### Set을 통해 알아보기
<pre><code>
const set = new Set([1,2,3]);
for (const a of set) log(a);
</code></pre>

### Map을 통해 알아보기
<pre><code>
const map = new Map([['a',1],['b',2],['c',3]]);
for (const a of map) log(a);
</code></pre>

## 이터러블/이터레이터 프로토콜
- 이터러블: **이터레이터를 리턴**하는 [Symbol.iterator]()를 가진 값
    - Array는 이터러블이라고 할 수 있다.
    - arr[Symbol.iterator] // null을 배정했을 때, 오류로 보아서 for of 문과 iterator가 연관이 있음을 알 수 있다.
- 이터레이터: { value, done } 객체를 리턴하는 next() 를 가진 값
- 이터러블/이터레이터 프로토콜: 이터러블을 for...of, 전개 연산자 등과 함께 동작하도록한 규약

