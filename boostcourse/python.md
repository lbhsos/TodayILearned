zip 사용하기
------
<pre><code>
for i in range(n):
    for j in range(n):
        new_map[j][i] = origin_map[i][j]
</code></pre>

행과 열을 바꾸는 연산 수행시 c 혹은 JAVA 같은 경우는 위와 같이 작성할 수 있다. 반면 파이썬은 **zip** 을 사용하여 다음과 같이 작성 할 수 있다.

<pre><code>
new_map = list(map(list,zip(*origin_map)))
</code></pre>

'*'를 사용하여 origin_map을 unpacking 한 후, zip을 사용하여 열 별로 데이터를 묶어준다. 이에 list 함수를 적용한다는 뜻으로 map 라이브러리를 사용한다.


2차원을 1차원 리스트로 
-----

<pre><code>
방법 1
sum(my_list, [])

방법 2
import itertools
list(itertools.chain.from_iterable(my_list))

방법3
import itertools
list(itertools.chain(*my_list))

방법 4
[element for array in my_list for element in array]
</pre></code>

방법 4에서와 같이 한 줄로 for문을 작성할 경우, 앞에 나오는 for문 일수록 더 큰 반복문이다. (if문 추가 시, 해당 for문 영역 바로 뒤에 작성)


가장 많이 등장하는 알파벳 찾기
---------
보통은 dictionary를 이용해서 많이 찾지만, collection.Counter 클래스를 사용하면 간략하게 만들 수 있다.
collection.Counter 후, 찾고자 하는 수를 num이라고 표현하면 list[num] 사용시, 해당 num의 출현 빈도수를 리턴해준다.


가장 큰 수, inf
-------
<pre><code>
min_val = 999999 (X)
min_val = float('inf') (O)
min_val = float('-inf') (O)
</code></pre>

inf는 어떤 수와 비교할 경우 항상 더 크다고 판정한다.


n진법으로 표기된 string 을 10진법 숫자로 변환
--------
파이썬의 int(x, base = 10) 함수는 진법 변환을 지원한다.


순열과 조합
-----
<pre><code>
import itertools
itertools.permutations(list, n)
itertools.combinations(list, n)
</pre></code>

문자인지 숫자인지!
-----
문자인지는 list.isalpha(), 숫자는 var.isdigit() 다음과 같이 사용할 수 있다.

python list 사용시 주의할점!
-------
python으로 코딩테스트 할 때, 주의할 점!
- list remove를 하게되면 index out of range 혹은 값 참조가 애매해질 수 있다.
- 이를 위해서 삭제 후 다시 참조하게 될 때는 다른 스택, 큐, 리스트 자료구조를 사용하여 보관용으로 사용하는 것도 좋다.
- 마지막 참조위치를 기억할 때는 별도의 지역변수를 사용한다. 예를 들어, idx와 같은 변수 이용시 for문을 돌 때 arr[idx:] 다음과같이 표현하면, arr의 idx 인덱스부터 끝가지 참조 가능하다.


dictionary merge
-----
일반적으로 python3.x 이상부터 지원되는 dictionary 합치기 방식은 다음과 같다. 
<pre><code>
dict(dict2, **dict1)
  
dict1이 dict2를 덮어쓴다. **는 kwargs(=keyword argument)를 뜻함.
</code></pre>

두 개의 dictionary 를 합칠 때, dictionary 기준이 아닌 값을 기준으로 새로운 dictionary를 만들고자 한다면 다음과 같이 표현할 수 있다.
<pre><code>
union_dict = {k : min(i for i in (str1_dict.get(k), str2_dict.get(k)) if i) for k in str1_dict.keys() | str2_dict}
</code></pre>

다음과 같은 코드는 str1_dict와 str2_dict를 돌며, 둘 중 더 큰 값을 해당 key에 배정하는 코드이다. 
str1_dict.keys() | str2_dict 는 key의 합집합을 의미한다.

  
이와 같은 식을 이용하면 아래와 같이 두 dictionary에 모두에 있는 키 값중 가장 작은 값을 사용하는 식을 여러줄에 거치지 않고 한 줄로 표현할 수 있다.

<pre><code>
for str1_key in str1_dict.keys():
        for str2_key in str2_dict.keys():
            if str1_key == str2_key:
                inter_dict[str1_key] = min(str1_dict[str1_key], str2_dict[str2_key])
</code></pre>

<pre><code>
inter_dict = {k: min(i for i in (str1_dict.get(k), str2_dict.get(k)) if i) for k in str1_dict.keys() & str2_dict}
</code></pre>

datetime 모듈 알아보기
-------
- *시간*을 *문자열*로 출력하려면 **strftime** 메서드를 사용한다.
- *날짜*, *시간*형식의 문자열을 *datetime*으로 만들 때는 **strptime**을 사용하면 된다.
- 날짜, 시간 연산을 할 때는 **datetime.timedelta**를 이용한다.
|단위|Method|
|:---|:---|
|1주|datetime.timedelta(weeks=1)|
|1일|datetime.timedelta(days=1)|
|1시간|datetime.timedelta(hours=1)|
|1분|datetime.timedelta(minutes=1)|
|1초|datetime.timedelta(seconds=1)|
|1밀리초|datetime.timedelta(milliseconds=1)|
|1마이크로초|datetime.timedelta(microseconds=1)|

> timedelta로 5시간 30분을 표현하면
- datetime.timedelta(hours=5, minutes =30)

시간, 분을 이용하고자 하는데 strftime을 사용하면 앞의 연, 월, 일은 default값으로 구성하게 된다. 따라서, 시간만 이용하거나 날짜만 이용할 때는 datetime.time 또는 datetime.date 를 이용한다. 이후 문자열에서 datetime 객체가 되면, **strftime**을 이용하여 formatting을 사용하면 된다.


python input 
-------
갯수를 알 수 없는 input 이 필요하다면, 다음과 같이 표현할 수 있다.
<pre><code>
import sys
for line in sys.stdin:
        print(line)
</code></pre>

만약, 파일이름을 커맨드라인 argument로 받아서 파일을 읽을 때는 fileinput 모듈이 좋다. 파일이름이 주어지면 파일을 읽어주고 아무것도 안주어지면 stdin에서 읽는다.
<pre><code>
import fileinput
for line in fileinput.input()
        pass
</code></pre>

> 종료시에는 sys.exit() 사용

split()
------
sep와 maxsplit은 기본값으로 각각 공백과 1이 저장되어있다. sep에는 기준, maxsplit은 문자열을 몇 번 쪼갤것인지 입력한다.