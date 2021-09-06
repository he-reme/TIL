# AJAX

> Asynchronous Javascript And XML
>
> 비동기적인 방식

#### Ajax 소개

* 언어나 프레임워크가 아닌 구현하는 방식을 의미
* 웹에서 **화면을 갱신하지 않고 데이터를 서버로부터 가져와 처리하는 방법**을 의미
  * 데이터 형식
    * XML
    * JSON ★
    * CSV
* JavaScript의 XMLHttpRequest(XHR) 객체로 **데이터를 전달하고 비동기 방식으로 결과를 조회**
* 화면 갱신이 없으므로 사용자 입장에서는 편리하지만, 동적으로 DOM을 구성해야 하므로 구현이 복잡

<br>

#### 일반 요청 vs Ajax 요청

* 일반 요청에 대한 응답
  * data를 입력 후 event 발생
  * Ajax를 적용하지 않은 요청은 서버에서 data를 이용하여 logic 처리
  * logic 처리에 대한 결과에 따라 응답 page(html)을 생성하고 client에 전송
    * 화면 전환이 일어남
* Ajax 요청에 대한 응답
  * data를 입력 후 event 발생
  * Ajax를 적용하면 event 발생 시 서버에서 요청을 처리한 후 Text, XML, JSON으로 응답
  * client(Browser)에서는 이 응답 data를 이용하여 화면 전환없이 현재 페이지에서 동적으로 화면을 재구성

<br>

#### AJax 사용하기

* Javascript
* JQuery
* Axios

<br>

---

<br>

## Javascript AJAX

* XMLThhpRequest

  * 자바스크립트가 Ajax 방식으로 통신할 때 사용하는 객체
  * Ajax 통신 시 전송방식, 경로, 서버로 전송할 data 등 전송 정보를 담는 역할

* 실제 서버와의 통신은 브라우저의 Ajax 엔진에서 수행

* 직접 자바스크립트로 Ajax를 프로그래밍할 경우 브라우저 별로 통신 방식이 달라 코드가 복잡해짐

  * 그래서 이거 사용
    * `var httpRequest = getXMLHttpRequest();`

* `httpRequest.js`

  ```javascript
  function getXMLHttpRequest(){
  	if(window.ActiveXObject){
  		try{
  			return new ActiveXObject("Msxml2.XMLHTTP");
  		}catch(e1){
  			try{
  				return new ActiveXObject("Microsoft.XMLHTTP");
  			}catch(e2){
  				return null;
  			}
  		}
  	}else if(window.XMLHttpRequest){
  		return new XMLHttpRequest();
  	}else{
  		return null;
  	}
  }
  
  var httpRequest = null;
  
  function sendRequest(url, params, callback, method){
  	httpRequest = getXMLHttpRequest();
  	
  	var httpMethod = method ? method : 'GET';
  	if(httpMethod != 'GET' && httpMethod != 'POST'){
  		httpMethod = 'GET';
  	}
  	var httpParams = (params == null || params == '') ? null : params;
  	var httpUrl = url;
  	if(httpMethod == 'GET' && httpParams != null){
  		httpUrl = httpUrl + "?" + httpParams;
  	}
  	
  	//alert("method == " + httpMethod + "\turl == " + httpUrl + "\tparam == " + httpParams);
  	httpRequest.open(httpMethod, httpUrl, true);
  	httpRequest.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
  	httpRequest.onreadystatechange = callback;
  	//alert(httpMethod == 'POST' ? httpParams : null);
  	httpRequest.send(httpMethod == 'POST' ? httpParams : null);
  }
  ```

  

<br>

#### httpRequest의 속성값

* `readyState`
  * `0` ~ `3`
    * 데이터를 전부 받지 않은 상태 (로딩중)
  * `4`
    * 데이터를 전부 받은 상태

* `status`
  * `200`
    * 요청 성공
  * `403`
    * 접근 거부, 클라이언트 실수
  * `404`
    * 페이지 없음, 클라이언트 실수
  * `500`
    * 서버 오류 발생, 개발자 실수

* 사용

  ```javascript
  if(httpRequest.readyState == 4){
  	if(httpRequest.statuc == 200){
  		...
  	}
  } else {
  	// 로딩중~
  }
  ```

<br>

---

<br>

## jQuery Ajax

* `httpRequest.js` 필요 없음
* jQuery 내장으로 지원해줌

<br>

#### `$.ajax(option);` 

* jQuery에서 Ajax 기능을 제공하는 가장 기본적인 함수

* 다른 함수들에 비해 옵션을 다양하게 지정할 수 있으며 실무에서 가장 많이 사용됨

* 함수의 옵션은 다양하지만 대부분 자동으로 지정하므로 생략 가능

* 옵션 (지정해줘야 하는 옵션들)

  * `url`
    * 대상 URL 지정
    * 자료형 : String
  * `data`
    * 요청 매개변수 지정
    * 자료형 : Object, String
  * `type`
    * 'GET' 또는 'POST' 등을 지정
    * 자료형 : String
  * `success(data, status, xhr)`
    * Ajax 성공 이벤트 리스너를 지정
    * 자료형 : Function
    * `data` : 값을 가져옴

  * `error(xhr, status, error)`
    * Ajax 실패 이벤트 리스너를 지정
    * 자료형 : Function

* 예시

  ```javascript
  $.ajax({
  	url: 'example.jsp',
      type: 'GET',
      success: function (response) {
      	$('#curtime').addClass('viewtime').empty().append(response);
      },
      error: function (xhr, status, msg) {
      	console.log('상태값 : ' + status + ' Http에러메시지 : ' + msg);
      },
  });
  ```

<br>

#### `$.get()`, `$.post()`

* `$.get()`, `$.post()` 함수는 $.ajax()의 옵션 속성 중 type 옵션이 지정된 함수

* 지정된 HTTP Method로 Ajax 통신을 함

  * `get()` : GET 방식
  * `post()` : POST 방식

* 사용

  ```javascript
  $.xxx(url, function(result, textStatus, jqXHR){});
  $.xxx(url, data, function(result, textStatus, jqXHR){});
  ```

<br>

#### 참고

* GET 방식 특징
  * URL에 변수(데이터)를 포함시켜 요청
  * 데이터를 Header(헤더)에 포함하여 전송
  * URL에 데이터가 노출되어 보안에 취약함
  * 전송하는 길이에 제한이 있음
  * 캐싱 할 수 있음
    * 캐싱 : 한번 접근 후, 또 요청할 시 빠르게 접근하기 위해 레지스터에 데이터를 저장시켜 놓는 것
* POST 방식 특징
  * URL에 변수(데이터)를 노출하지 않고 요청
  * 데이터를 Body(바디)에 포함시킴
  * URL에 데이터가 노출되지 않아 기본 보안은 되어있음
  * 전송하는 길이에 제한이 없음
  * 캐싱 할 수 없음

<br>

#### `$(selector).load()`

* 서버로부터 내용을 조회하여 선택자를 통해 탐색한 DOM 객체에 동적으로 삽입

* 일반적으로 잘 사용하진 않음

* 인자

  * url : 필수 값으로 HTML을 조회할 서버 URL을 지정
  * data : 요청 시 서버에 전달할 데이터를 지정
  * function : 서버와 통신을 완료한 후에 수행할 콜백함수를 지정

* 사용

  ```javascript
  $(selector).load(url);
  $(selector).load(url, data, function(result, textStatus, jqXHR){});
  ```

<br>

---

<br>

## 데이터 전송 형식

* server와 client는 주고 받을 data의 형식을 맞춰야 함
* 대표적인 data의 형식
  * CSV, XML, JSON


<br>

#### CSV

* Comma Separated Values
* 각 항목을 쉼표`,`로 구분해 데이터를 표현하는 방법
* 다른 두 형식에 비해 굉장히 짧음. 많은 양의 데이터 전송 시 유리함
* 단, 각각의 데이터가 어떤 내용인지 파악하기 어려움
  * 서버와 클라이언트가 완벽히 데이터 구조를 공유할 경우엔 가능
* **모든 데이터의 콤마의 갯수가 동일할 때 사용!!!**
  * 다르면 사용하기 어려움 
* 예
  * 2020111,김싸피,A,90
  * 2020112,홍싸피,B,92

<br>

#### XML

* eXtensible Markup Language

* xml은 tag로 data를 표현함

* tag를 보면 각 data가 무엇을 의미하는지 파악 가능

* tag에 사용자 정의 속성을 넣을 수 있으므로 복잡한 data 전달 가능

* 예시

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  
  <students>
  	<student>
  		<id>20201111</id>
  		<name>김싸피</name>
  		<class>A</class>
  		<grade>90</grade>
  	</student>
  	<student>
  		<id>20201112</id>
  		<name>홍싸피</name>
  		<class>B</class>
  		<grade>92</grade>
  	</student>
  	<student>
  		<id>20201113</id>
  		<name>박싸피</name>
  		<class>C</class>
  		<grade>91</grade>
  	</student>
  </students>
  ```

<br>

#### JSON

* JavaScript Object Notation

* CSV와 XML의 단점 극복한 형식

* Javascript에서 사용하는 객체의 형식으로 data를 표현

* Ajax 사용시 거의 표준으로 사용되는 data 표현 방식

* 예시

  ```json
  [
   {
   	"id" : "20201111",
   	"name" : "김싸피",
   	"class" : "A",
   	"grade" : "90"
   },
   {
   	"id" : "20201112",
   	"name" : "홍싸피",
   	"class" : "B",
   	"grade" : "92"
   },
   {
   	"id" : "20201113",
   	"name" : "박싸피",
   	"class" : "C",
   	"grade" : "91"
   }
  ]
  ```

<br>

---

<br>

## Event 관리

> 전역 함수

* Ajax는 서버와 통신하는 과정이 웹 브라우저 내부에서 이루어지므로 사용자가 진행상황을 알기 어려움

* Ajax 전역함수를 사용하여 Ajax 처리 중에 진행 상태를 보여주는 기능을 구현할 수 있음

  * 로딩중?? 클라이언트에게 알려줄 때

* jQuery는 Ajax 처리가 이루어지는 각 단계 별로 전역함수를 호출함

  * 단, jQuery의 전역함수는 `$.ajaxSetup()` 함수에 `global `속성 설정이 `true`인 경우에만 수행됨
    * 디폴트 : `true`

* 사용 예시

  ```javascript
  $(document)
  .ajaxStart(function(){
  
  })
  .ajaxStop(function(){
  
  });
  ```

<br>

#### 전역 함수

* `ajaxStart` ★

* `ajaxSend`
* `ajaxSuccess`
* `ajaxError`
* `ajaxComplete`
* `ajaxStop` ★

