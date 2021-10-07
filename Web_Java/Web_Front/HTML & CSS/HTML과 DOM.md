## HTML과 DOM

#### DOM

* Document Object Model
* HTML과 XML문서의 구조를 정의하는 API 제공
* 문서 요소 집합을 트리 형태의 계층 구조로 HTML을 표현
  * HTML 계층 구조의 제일 위에는 `document` 노드가 있음
  * 그 아래로 HTML 태그나 요소(element)들을 표현하는 노드와 문자열을 표현하는 노드가 있음
    * element node :  `<>`
    * text node : "제목입니다."

<br>

#### 문서 계층구조

* Document는 HTML 또는 XML 문서를 표현
* HTML Document는 HTML 문서와 요소만을 표현
* HTMLElement의 하위 타입은 HTML 단일 요소나 요소 집합의 속성에 해당하는 JavaScript 프로퍼티를 정의
* Comment 노드는 HTML이나 XML 주석을 표현

<br>

#### 문서 객체 만들기

* **구분**
  * text node를 갖는 객체
  * text node를 갖지 않는 객체

* **함수**

  * `createElement(tagName)`
    * element node를 생성
  * `createTextNode(text)`
    * text node 생성
  * `appendChild(node)`
    * 객체에 node를 child로 추가

* 예시

  ```javascript
  window.onload = function(){
  	// 변수를 선언하고 element node와 text node 생성
  	var title = document.createElement('h2');
  	var msg = document.createTextNode('hello hyerim');
  	
  	// text node를 element node에 추가
  	title.appendChild(msg);
  	document.body.appendChild(title);
  };
  ```

<br>

#### 문서 객체 속성 설정

* 함수

  * `setAttribute(name, value)`
    * 객체의 속성을 지정
  * `getAttribute(name)`
    * 객체의 속성값을 가져옴

* 예시

  ```javascript
  window.onload = function(){
  	var profile = document.createElement('img');
  	
  	profile.setAttribute('src', 'profile.png')l
  	profile.setAttribute('width', 150);
  	
  	profile.setAttribute('data-content', '내사진')
  	
  	document.body.appendChild(profile);
  };
  ```

<br>

#### 문자열 삽입

* 속성

  * `innerHTML`
    * 문자열을 **HTML 태그로 삽입**
  * `innerText`
    * 문자열을 **text node로 삽입**

* 예시

  ```javascript
  window.onload = function() {
  	var html = document.getElementById('divHtml');
  	var text = document.getElementById('divText');
  	
  	html.innnerHTML = '<h2>Hello HyeRim</h2>';
  	text.innerText = 'Hello HyeRim';
  };
  ```

<br>

#### 문서 객체 가져오기 ★★★

* 함수
  * `getElementById(id)`
    * 태그의 id 속성이 id와 일치하는 **element 객체 얻기**
  * `getElementsByClassName(classname)`
    * 태그의 class 속성이 classname과 일치하는 **element 배열 얻기**
  * `getElementsByTagName(tagname)`
    * 태그 이름이 tagname과 일치하는 **element 배열 얻기**
  * `getElementsByName(name)`
    * 태그의 name 속성이 name과 일치하는 **element 배열 얻기**
  * `querySelector(selector)`
    * selector에 일치하는 **첫 번째 element 객체 얻기**
    * `.`, `#` 등 사용해줘야 함
  * `querySelectorAll(selector)`
    * selector에 일치하는 **모든 element 배열 얻기**
    * `.`, `#` 등 사용해줘야 함

* 사용
  * `document.XXXX()`
  * element 배열 사용하기
    * `arr[index]`

<br>

#### 문서 객체 제거

* 속성

  * `removeCild(childnode)`
    * 객체의 자식 노드 제거

* 예시

  ```javascript
  window.onload = function(){
  	var a = document.querySelector('#h6_a');
  	document.body.removeChild(a); // body 태그 안의 a노드 삭제
  };
  ```

<br>