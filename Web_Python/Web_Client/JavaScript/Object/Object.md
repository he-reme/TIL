# 객체

> 이름과 값을 가진 data의 집합 및 data를 조작하기 위한 Method가 하나로 묶인 것

* 동적으로 객체의 속성과 메서드를 추가하거나 삭제 가능
* 상속구문도 적용할 수 있음

* `this` 객체

  * 함수가 객체의 메서드로서 불리게 되면, `this`는 메소드를 부른 객체로 설정됨

  * 함수가 단독으로 호출되면, `this`는 기본적으로 브라우저의 `window`객체가 됨

  * 함수명으로 호출 가능한 `call()`과 `apply()` 메서드를 사용해도 함수 호출이 가능

    * 이 경우에는, 함수내에서 사용되는 `this`가 어떠한 객체를 참조하게 될지 자유롭게 설정 가능

    

---



## 객체 정의 방법 및 활용

### 1. 객체 리터럴 사용

#### (1) 정의 방법

```javascript
var 객체명 = {
	속성명 : 속성값,
	속성명 : 속성값,
	...
	속성명 : function(){}
}
// 객체명.속성명
// 객체명.속성명() : 함수의 경우
```

* 재사용 없음

#### (2) 정의 예시

```javascript
var student = {
	name : "혜림",
	kor : 90,
	eng : 80,
	math : 95,
	getSum : function(){
		return this.kor + this.eng + this.math;		
	}
	getAvg : function(){
		return this.getSum() / 3;
	}
}
```

* 추가적인 예시 (이중)

  ```javascript
  var user = { father : {name : "고길동",age : 40}, son : {name : "희동이",age : 2} }
  // user.father.name
  // user.son.name
  ```

  

#### (3) 속성 추가하기

```javascript
student.age = "25";
student.getName = function(){
	return this.name;
}
```

#### (4) 속성 제거하기

````javascript
delete student.age;
delete student.getName;
````



### 2. 생성자 함수를 사용

#### (1) 정의 방법

```javascript
function 함수명([매개변수])
{
	this.속성명 = 값;
	this.속성명 = 값;
	...
}
// var 객체명 = new 함수명()
// 객체명.속성명
// 객체명.속성명() : 함수의 경우
```

* 재사용 가능
* 자바스크립트의 함수
  * 실행 가능한 코드와 연결된 객체!
* 함수명의 첫 글자는 대글자로 사용

#### (2) 정의 예시

* 메소드가 안에

  ```javascript
  function Student(name, kor, eng, math){
  	this.name = name;
  	this.kor = kor;
  	this.eng = eng;
  	this.math = math;
  	this.getName = function(){
  		return this.name;
  	}
  	this.getSum = function(){
  		return this.kor + this.eng + this.math;
  	}
  	this.getAvg = function(){
  		return this.getSum()/3;
  	}
  }
  var st = new Student("혜림", 100, 100, 100);
  ```

* 메소드가 밖에 (1) - prototype 속성 사용

  ```javascript
  function Student(name, kor, eng, math){
  	this.name = name;
  	this.kor = kor;
  	this.eng = eng;
  	this.math = math;
  }
  Student.prototype.getName = function(){
  		return this.name;
  }
  Student.prototype.getSum = function(){
  		return this.kor + this.eng + this.math;
  }
  Student.prototype.getAvg = function(){
  		return this.getSum()/3;
  }
  var st = new Student("혜림", 100, 100, 100);
  ```

* 메소드가 밖에 (2)

  ```javascript
  function Student(name, kor, eng, math){
  	this.name = name;
  	this.kor = kor;
  	this.eng = eng;
  	this.math = math;
  	this.getName = getName;
  	this.getSum = getSum;
  	this.gtAvg = getAvg;
  }
  function getName{
  	return this.name;
  }
  function getSum{
  		return this.kor + this.eng + this.math;
  }
  function getAvg{
  		return this.getSum()/3;
  }
  var st = new Student("혜림", 100, 100, 100);
  document.write(st.getName());
  ```

  

---



## 표준 내장 객체 종류

> 자바스크립트 언어 자체에 정의되어어 있는 객체

### window 객체

#### (1)  JavaScript

* 종류
  * Object, Array, Function, String, Boolean, Numbr
  * Math : 수학 함수 기능 제공
  * Date : 날짜와 시간 정보 추출, 설정 관련 기능 제공
  * RegExp : 정규 표현식(패턴)을 이용하여 데이터를 처리하려는 경우 사용됨

####  (2) DOM (Document Object Model)

* 종류
  * document

#### (3) BOM (Browser Object Model)

* 종류
  * navigator, screen, location, frames, history
  * (나중에 BOM 할때 수정하장~) 
    * location.href = "URL" : 현재 페이지에서 해당 URL로 이동



---



## DOM

> Document Object Model
>
> 모든 브라우저는 이 DOM 객체를 

* 브라우저가 웹페이지(HTML)를 해석하고 랜더링할 때,

  *  인식된 각각의 태그들을 자바스크립트 객체로 생성하며 
  * 이 객체들을 DOM 객체라고 함.

* 생성되는 DOM 객체들은 부모 자식 관계를 적용하여 트리구조로 구성됨

  * document - body - ...

  * 그래서 일반적으로 `<body> 태그`에 접근하고 싶으면 `document.body` 로 접근하면 됨 

  * 예시

    ```html
    <body>
    	<h1> ... </h1>
    	<ol>
    		<li> ... </li>
    		<li> ... </li>
        </ol>
    </body>
    ```

  * 예시의 계층구조

    ```
    	document
    	  body
     h1          ol
    ...       li     li
             ...     ...
    ```



### DOM 객체 타입

* Element 타입
* Attribute 타입
* Text 타입
* 등



---



## window

* `window.alert("메시지")` 
  
* 사용자에게 메시지를 보여주고 확인받는 용도
  
* `window.prompt()`
  
  * 사용자로부터 데이터를 입력받는 용도
  
* `window.confirm('원하는 메시지를 입력')`
  
  * `예` 또는 `아니오` 둘 중 하나를 입력받는 용도
    * 예 : `true`
    * 아니오 : `false`
  
* `window.setInterval(함수, time)`

  * `time`마다 함수를 실행시킴

    ```javascript
    var displayDate = function()
    {
    	var d = new Date();
    	document.write(d.toLocaleString()+"<br>");
    };
    var time = 5000; //5초
    window.setInterval(displayDate,time);
    ```

    
  

## document

> 자바스크립트 내장 객체

####  `document.write()`

* 괄호 안의 내용을 브라우저에 출력

* **개행 비포함**

* 예시1

  ```javascript
  var v1 = "hello";
  document.write(v1 +"<br>");
  ```

  * `태그`를 넣어서 사용할 수 있음
    * `""` 를 사용

* 예시2

  ```javascript
  document.write("<ul>");
  var v1;
  document.write("<li>"+ v1 +"</li>"); // undefined
  document.write("<li>"+ typeof v1 +"</li>"); // undefined
  document.write("<li>"+ (v1+10) +"</li>"); // NaN (=Not a Number)
  v1 = 100;
  document.write("<li>"+ v1 +"</li>");
  document.write("<li>"+ typeof v1 +"</li>");
  document.write("<li>"+ (v1+10) +"</li>");
  v1 = true;
  document.write("<li>"+ v1 +"</li>");
  document.write("<li>"+ typeof v1 +"</li>");
  document.write("<li>"+ (v1+10) +"</li>");
  v1 = "가나다";
  document.write("<li>"+ v1 +"</li>");	
  document.write("<li>"+ typeof v1 +"</li>");
  document.write("<li>"+ (v1+10) +"</li>");
  document.write("<ul>");
  ```



#### (3) `document.writeln()`

* 괄호 안의 내용을 브라우저에 출력
* `document.write()` 와 다르게 **개행 포함**




