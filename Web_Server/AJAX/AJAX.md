# AJAX

> Asynchronous JavaScript and XML



* 인스타그램, 페이스북과 같은 사이트 만드는데 사용
* 웹은 기본적으로 동기 통신
  * 요청을 보내면 응답을 받을 때 까지 기다림

* AJAX를 이용하면 동기, 비동기 통신을 선택할 수 있음
  * 요청을 보내고 다른 일을 할 수 있음

* JSON과 XML 형식으로 주고받음
  * 주로 JSON 사용



#### 목차

* 고전 vs AJAX
* AJAX 원리
* AJAX의 동작 과정
* AJAX 프로그래밍 핵심 내용
* JavaScript 사용
* JQuery API 사용



---



## 고전 vs AJAX

> 비교

#### 고전적 웹 통신

* 동기 통신
* 요청을 보내면 응담을 받을 때까지 대기
* 웹페이지의 일부분을 갱신하기 위해서는 페이지 전체를 다시 로드해야 함

#### AJAX를 이용한 웹 통신

* 동기, 비동기 통신 선택 가능
* 요청을 보내고 다른 일을 할 수 있음
* **재로드(refresh 재갱신) 하지 않고 웹페이지의 일부분만을 갱신**하여 웹서버와 데이터를 교환
* 즉, **빠르게 동적 웹페이지를 생성하는 기술**

  


---



## AJAX 원리

> 웹 페이지의 **디자인 요소**와 **정보 요소**를 **분리**!!!

* 브라우저가 사이트에 접속하면

* 서버는 사이트의 기본 얼개를 담은 **템플릿**을 전달

* 브라우저는 수신받은 템플릿을 해석해 화면의 기본 모양을 그림

  * 정적 HTML 파일
  * CSS 파일

* 브라우저는 JavaScript 파일을 해석해서 파일에 기술된 방식대로 서버에 추가 데이터를 요청

  * JavaScript 파일 : 데이터를 어떻게 요청하면 되는지를 설명한 파일

* 서버는 순수 데이터(순수 객체 데이터)를 응답으로 되돌려줌

  * **XML** 또는 **JSON**
    * 주로 JSON

* 브라우저는 수신한 데이터를 해석하여 템플릿의 적절한 위치에 삽입

  * 데이터의 가공 방식에 따라 삽입 외의 작업(변경, 삭제)을 할 수 있음

  

---



## AJAX의 동작 과정

1. 이벤트 발생에 의해 이벤트 핸들러 역할의 JavaScript 함수를 호출
2. 핸들러 함수에서 `XMLHttpRequest 객체`를 생성하고, 요청이 종료되었을 때 처리할 기능을 콜백함수로 만들어 등록
3. `XMLHttpRequest 객체`를 통해 서버에 요청을 보냄
4. 요청 받은 서버는 요청 결과를 적당한 데이터로 구성하여 응답
5. `XMLHttpRequest 객체`에 의해 등록된 콜백 함수를 호출하여 응답 결과를 현재 웹 페이지에 반영



---



## AJAX 프로그래밍 핵심 내용

1. JSON(XML) 형식으로 응답하는 뷰를 준비해야 함.

   * 템플릿을 거치지 않고 뷰가 직접 응답
   * 템플릿을 거치지 않고 = html 파일 없음

2. AJAX 요청 구현 방법 (2가지)

   * JavaScript 사용

     ```javascript
     var xhr = new XMLHttpRequest() // XMLHttpRequest객체 생성
     xhr.onload = 함수 // 이벤트 핸들러 등록
     xhr.open("GET", 대상URL, true)
     xhr.send()
     ```

   * jQuery API 사용

     ```
     $.getJSON("대상URL", 함수) // 대부분 아래보다 이것을 사용
     ```

     * 대상 URL  실행 후, 함수가 호출됨

     ```
     $.ajax({...............})
     ```



---



## JavaScript 사용

#### `open()` 메서드

```javascript
open(HTTP 메서드, URL [, 비동기 모드 통신 여부])
```

* HTTP 메서드

  * 요청 방식
  * GET, POST, DELETE

* URL

  * AJAX로 요청하려는 서버의 대상 페이지

* 비동기 모드 통신 여부

  * true
    * 비동기 통신
    * default 값

  * false
    * 동기 통신

#### `send()` 메서드

````javascript
send([요청 파라미터])
````

* POST의 경우 Query 문자열을 인수로 지정
* `ArrayBufferView, Blob, Document, DOMString, FormData, null `이 올 수 있음

#### XMLHttpRequest 객체에서 제공되는 이벤트 관련 속성

* onloadstart
* onprogress
* onabort
* onerror
* onload
* ontimeout
* onloadend
* onreadystatechange



---



## JQuery API 사용

> 이 방법을 많이 쓸거임~
>
> 아래는 AJAX 메소드들

#### `$.ajax()`

* 모든 AJAX 메소드의 기본이 되는 메소드

#### `$.get()`

* GET 방식의 AJAX 메소드

#### `$.post()`

* POST 방식의 AJAX 메소드

#### `$.getJSON()`

* JSON 형식으로 응답 받는 AJAX 메소드

#### `$().load()`

* 서버로부터 데이터를 받아서 일치하는 요소 안에 HTML을 추가

#### `$.getScript()`

* 자바스크리트 형식으로 응답 받는 AJAX 메소드

#### `$.ajaxSetup()`

* AJAX 메소드의 선택 사항들에 대한 기본값 설정



---



## `$.ajax()`

* 모든 AJAX 메소드가 내부적으로 사용하는 기본 메소드

* AJAX 요청을 기본적인 부분부터 직접 설정하고 제어할 수 있어, 다른 AJAX 메소드로 할 수 없는 요청도 수행 가능

#### 기본 형식

```javascript
$.ajax(options);
```

#### options

```javascript
$.ajax({
	url: URL 주소,
	[type: 요청 방식,]
	[data: 요청 내용,]
	[timeout: 응답 제한 시간,]
	[dataType: 응답 데이터 유형,]
	[async: 비동기 여부,]
	[success: 성공 콜백 함수,]
	[error: 실패 콜백 함수]
});
```

* `url : URL 주소`
  * 요청이 보내질(주로 서버)의 URL 주소로, 필수항목
  * 기본값은 현재 페이지
* `type : 요청 방식`
  * 요청을 위해 사용할 HTTP 메소드
  * `get`,` post`
    * 기본값은 `get`
* `data : 요청 내용`
  * 서버로 전달되는 요청 내용(jQuery 객체맵이나 문자열)
* `timeout : 응답 제한 시간`
  * 요청 응답 제한 시간 (밀리초)

* `dataType : 응답 데이터 유형`
  * (서버로부터의) 반환될 응답 데이터의 형식
* `Async : 논리값`
  * 요청이 비동기식으로 처리되는지 여부
  * 기본값은 `true`
* `sucess : function(data)`
  * 요청 성공 콜백함수 (data: 서버 반환 값)
* `error :  function()`
  * 요청 실패 콜백함수

#### 예시

```


```



---



## `$.load()` 메서드

* 서버로부터 데이터를 받아오는 가장 간단한 메서드로 많이 이용
* 서버로부터 데이터를 받아 메서드를 실행하는 대상 엘리먼트에 직접 추가
* 복잡한 선택 사항을 설정하지 않고도 빠르고 간단하게 웹 페이지의 동적 갱신 가능
* 요청이 성공하면 메서드가 실행되는 대상 엘리먼트 내용이 서버에서 응답 받은 HTML5 마크업 데이터로 대체

#### 기본 형식

```
$.load(options);
```

#### options

```
$.load(url[,data][,function(data)]);
```

* `url`
  * 요청이 보내질 (주로 서버)의 URL 주소로, 필수항목
  * 기본값은 현재 페이지
* `data`
  * 서버로 전달되는 요청 내용 (jQuery 객체맵이나 문자열)
* `function(data)`
  * 요청 성공 콜백 함수 
  * data : 서버 반환 값

#### 예시

````

````



---



## 자원 접근

#### Same Origin Policy (SOP)

* 브라우저에서 보안상의 이슈로 동일 사이트의 자원만 접근해야 한다는 제약
* AJAX는 이 제약에 영향 받으므로 Origin 서버가 아니면 AJAX로 요청한 컨텐츠를 수신할 수 없음