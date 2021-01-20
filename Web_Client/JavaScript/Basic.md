# 기본

> 자바스크립트의
>
> 구조, 변수, 연산자, 제어문, 배열, 함수

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

* 객체로 취급
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



#### (2) 배열 활용

* `arr.concat(추가연결할배열)`

* `arr.join(구분문자)`

* `arr.slice(시작[,끝])`

* `arr.pop()`

* `arr.push(요소)`

* `arr.shift()`

* `arr.unshift(요소, ...)`

* `arr.reverse()`

* `arr.sort([fnc])`

* `arr.toString()`

  

  



---



## 함수

* * `function()` : 함수
    * 함수명 생략 
      * like 람다 함수
    * 함수명 생략 X
      * 함수명 만들어 사용하면 HTML 태그에 정의된 속성 값으로 작성 가능



#### 난수 생성

* `Math.random()`

  ```javascript
  var rand = Math.random();
  ```

  * `0.0 <= rand < 1.0

* `0~N-1`사이의 난수를 생성하고 싶을 때

  ````javascript
  var rand = Math.random();
  var N = 3;
  document.writeln(Math.floor(rand*N))
  ````

