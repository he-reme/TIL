# 기본

> 자바스크립트의
>
> 구조, 변수, 연산자, 제어문, 배열, 함수

* 프로그램 실행 시 자바스크립트 엔진이 가장 먼저 파악하는 것 : 선언적 함수, 전역변수



---



## 구조

#### (1) `<script>` 태그 내부에 작성

```html
<script>
	<!-- 자바스크립트 구현 -->
</script>
```

* 문장 마지막에 `;`세미콜론 사용
* 가급적 `<script></script>` 는 `</head>` 위에 삽입하여 작성하기
  * 랜더링 이전에 이것이 브라우저에 의해 먼저 해석되면 랜더링을 지연시키는 결과가 될 수 있기 때문!

#### (2) HTML 태그에 정의된 속성 값으로 작성

```javascript
<button onclick="displayDate('red')">빨강</button> // 이런식으로
<button onclick="displayDate('blue')">파랑</button>
<button onclick="displayDate('yellow')">노랑</button>
<hr>
<output id="target"></output>
<script>
    function displayDate(colorname) {
        var now = new Date();
        var strnow = now.getFullYear()+"년 " + (now.getMonth()+1)+"월 " + now.getDate()+"일";
        var targetDom = document.getElementById("target");
        console.log(targetDom);
        targetDom.textContent = strnow;
        targetDom.style.color = colorname;
    }
</script>
```



* 주석

  ```javascript
  // 이렇게 하거나
  /* 이렇게 하거나 */
  ```



---



## 변수

### 선언

```javascript
var 변수명;
var 변수명 = 값;
```

* variable



### 변수 타입

> 1. 기본형 타입
> 2. 객체 타입

* 타입 확인

  ```javascript
  typeof 변수 
  ```

  * 타입 종류 

    ```javascript
    "number", "string", "function", "boolean", "object"
    ```

  * `숫자 문자열`도 `숫자`로 취급하여 확인하고 싶을 때

    ```javascript
    isNaN(변수) // Not a Number
    ```

    * 숫자가 아니면 `true`
    * 숫자가 맞으면 `flase`

    

#### 1. 기본형 타입

#### (1) number

* 숫자

* `isNaN(변수)`

  * **숫자**가 될 수 있는 변수인지 확인하는 함수
  * `true`, `false` 반환

  

#### (2) string

* 문자열

* `' '` ,`" "` 둘 다 사용해도 상관 없음

* `문자열 + 문자열이 아닌 변수` = `문자열`!! 
  * 문자열이 아닌 변수를 문자열과  `+` 기호를 사용해서 연결하면 자동으로 문자열로 결합함

#### (3) boolean

* bool

* `true`
* `false`

#### (4) undefined

* 변수에 값이 안들어가있을 때



#### 2. 객체 타입

이에 대한 내용은 `Object.md` 에서 확인!



---



## 연산자

#### (1) 수치 연산자

* 기본 연산자 : `+` `-` `*` `/` `%`  

* 중가 연산자 : `++` `--` 

* 단항 연산자 : `-` 

* 문자열 연산자 :  `+`
  * 문자열을 합하여 하나의 문자열 생성
  * `문자열 + 문자열이 아닌 변수` = `문자열`
    * 문자열이 아닌 변수를 문자열과  `+` 기호를 사용해서 연결해도
    * 자동으로 문자열로 결합됨!!

#### (2) 비교 연산자

* `>` `<` `>=` `<=` `==` `===` `!=` `!==`

  * `==` 

    ```javascript
    document.writeln("100" == 100); // true
    ```

    * 타입 비교 안함, **값**만 비교

  * `===`

    ```javascript
    document.writeln("100" == 100); // false
    ```

    * **타입, 값** 모두 비교

#### (3) 조건 연산자

* AND 연산자 : `&&;
* ? 연산자 : `?`

#### (4) 대입 연산자

* `=` `+=` `-=` `*=` `/=` `%=`

#### (5) 비트 연산자

* 비트 AND : `&`
* 비트 OR : `|`
* 비트 XOR : `^`
* 비트 좌우 이동 : `<<` `>>`

#### (6) 타입 점검 연산자

* `typeof` `instanceof`

#### (7) 삭제 연산자

* `delete`



---



## 제어문

> c++과 사용법이 유사함!

#### (1) 조건 제어문 

* `if` `else` `else if` 
* 다중 분기문: `switch`

#### (2) 반복 제어문

* `for` (일반, 전통) 

  * `for(초기화식; 조건식; 증감식)`

    ```javascript
    for(var i=1; i<4; i++) // for문 초기화식에서 변수 선언 가능
    { 
        // 반복 수행 문장
    }
    ```

* `for` (향상된)

  * `for(변수정의 in 배열 또는 객체)`

    ```javascript
    a = [1, 2, 3, 4, 5];
    for(var i in a)
    {
    	document.writeln(a[i]); // 반복 수행 문장
    }
    ```
    * `i`에는 `a`의 요소가 꺼내지는 것이 아니라 **인덱스**가 꺼내짐
    * `0, 1, 2, 3, 4`

  * `for each`

* `while`
* `do-while`

#### (3) 분기 제어문

* `break`
* `continue`

#### (4) 에러처리 구문

* `try-catch-finally`



---



## 배열

> like 파이썬의 **리스트**

* **객체(Object)**로 취급
* 각 데이터들 = 요소
* 배열의 요소 갯수는 가변적으로 처리 가능
  * 배열 생성 시 크기를 지정하더라도
  * 필요하다면 배열을 구성하는 요소의 개수를 늘릴 수 있음
* 배열에 저장할 수 있는 데이터 타입에 제한이 없음
  * 배열을 구성하는 각 요소마다 다른 타입의 데이터를 저장하고 사용하는 것 가능



#### (1) 배열 생성 방법 (2가지)

1. 배열 리터럴 사용

   ```javascript
   var arr1 = [1, 2, 3, 4, 5];
   var arr2 = ["hello", "world"];
   var arr3 = [];
   ```

2. `Array()` 생성자 함수 호출

   ```javascript
   var arr1 = new Array(1, 2, 3, 4, 5);
   var arr2 = new Array("hello", "world");
   var arr3 = new Array();
   ```



#### (3) 배열 속성

* `arr.length`
  * 배열 길이 반환

  

#### (2) 배열 메소드

* `arr.concat(추가연결할배열)`

* `arr.join(구분문자)`

* `arr.slice(시작[,끝])`

* `arr.pop()`

* `arr.push(요소)`

  * 맨마지막 요소 다음에 요소를 추가함

* `arr.shift()`

* `arr.unshift(요소, ...)`

* `arr.reverse()`

* `arr.sort([fnc])`

  * 배열의 요소 정렬

  * 함수 없는 정렬 (default) : 문자열 기반 정렬

    ```javascript
    var arr = ['둘리', '또치', '도우너', '희동이', '고길동']
    var new_arr = arr.sort();
    ```

  * 함수 있는 정렬 (숫자 기반 정렬)

    ```javascript
    var arr = [30, 11, 5, 27, 9]
    var new_arr = arr.sort(function(a, b){ return a-b;});
    ```

* `arr.toString()`

  * `,` 가 요소 사이사이에 붙어서 출력된다
  
* 그냥 출력해도 자동으로 `toString()` 호출됨
  
  * 위와 동일
  
  

---



## 함수

> 하나의 로직을 재실행 할 수 있도록 하는 것으로 코드의 재사용성을 높여줌
>
> 자바스크립트 함수도 일급 객체를 만족
>
> 이벤트 핸들러 구현하는데 사용
>
>  HTML 태그에 정의된 속성 값으로 작성 가능

* 함수를 변수에 담아서 사용(호출)할 수 있고, 함수 호출시 아규먼트로 전달 가능
* 함수가 값을 리턴하지 않으면 undefined가 자동으로 리턴됨.



#### (1) 함수 정의 방법

* 선언적(명시적) 함수 정의

  ```javascript
  function 함수명([매개변수1, 매개변수2, ...])
  {
  	// 함수 수행 코드
  }
  함수명(); // 함수 호출
  ```

* 표현식(익명) 함수 정의

  ```javascript
  var 함수명 = function([매개변수1, 매개변수2, ...])
  {
  	// 함수 수행 코드.
      // return 리턴값
  };
  함수명(); // 함수 호출
  ```

* 공통점 
  
  * 사용 방법, 호출 방법
* 차이점 
  * 선언적 함수
    * 프로그램 실행시 가장 먼저 파악되기 때문에, 함수 선언보다 호출이 먼저 나와도 실행됨.
  * 표현식 함수
    * 함수 선언보다 호출이 먼저 나오면 에러



#### (2) 인수

* 함수를 호출할  때 함수에 정의된 매개변수만큼 인수를 전달하지 않아도 호출 가능
  
* 대신 매개변수에 인수를 전달하지 않으면 해당 매개변수의 값은 `undefined`가 됨
  
* 가변인수

  * 함수 호출시 인수 갯수에 제한이 없는 함수

  * 가변인수 함수를 정의할 때는 매개변수 정의를 생략하고, 함수 호출시 자동으로 만들어지는 `arguments`라는 배열을 활용!

  * 예시

    ```javascript
    function test() {
    	document.write("아규먼트 갯수 : "+arguments.length+"<br>");
    	for(var i=0; i < arguments.length; i++) 
    		console.log(arguments[i]);
    }
    
    test(); 
    test(10);
    test(10,20); 
    test('a', 'b', 'c'); 
    test(1,2,3,4,5,6,7,8);
    ```

* 고계(고차) 함수

  * 함수를 데이터로 다루는 함수

  1. 함수 호출 시 함수를 인수로 전달 가능

     ```javascript
     function test(callback){
     	if(callback != undefined)
     		callback(3);
     };
     test(function(num)
     {
     	if(num%2==1)
     		alert(num + ':Odd');
     	else
     		alert(num + ':Even');
     });
     ```

  2. 리턴 값으로 함수 전달 가능

     ```javascript
     function test()
     {
     	return function(str)
     	{
     		alert(str+"!!");
     	};
     };
     var result = test();
     ```

  

#### (3) 여러가지 함수

##### 1. 난수 생성

* `Math.random()`

  ```javascript
  var rand = Math.random();
  ```

  * `0.0 <= rand < 1.0`

* `0~N-1`사이의 난수를 생성하고 싶을 때

  ````javascript
  var rand = Math.random();
  var N = 3;
  document.writeln(Math.floor(rand*N))
  ````
  
  * `Math.floor()` : 소수점 아래를 날려버리는 함수

* `1~10` 사이의 난수를 생성하고 싶을 때

  ```javascript
  var num = Math.floor(Math.random()*10)+1;
  ```

  

##### 2. 날짜 반환

```javascript
var d = new Date();
document.writeln(d.toString());
document.writeln(d);
```

* 자바스크립트는 자동으로 `toString()` 호출해줌