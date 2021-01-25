# DOM

> Document Object Model

* DOM 객체 타입
* DOM 객체 접근 방법
* DOM 객체의 내용 접근
* DOM 객체 편집
* 이벤트 모델

---



## DOM 객체 타입

* Element 타입
* Attribute 타입
* Text 타입
* 등



---



## DOM 객체 접근 방법

> 동적인 처리를 하려는 태그의 DOM 객체 찾는 방법
>
> * 값이 없다 : undefined
> * 객체가 없다 : null

* DOM 객체 배열 접근
  * `dom[index]`
* DOM 객체 배열 `0 index`만 리턴 받고 싶을 때
  * `var dom = document.getElementsbyTagName("태그명")[0]; `

#### (1) 태그명으로, DOM 객체 배열 리턴

```javascript
var dom = document.getElementsbyTagName("태그명"); 
```

#### (2) 태그에 정의된 id 속성의 값으로, DOM 객체 리턴

```javascript
var dom = document.getElementbyId("id속성값");
```

#### (3) 태그에 정의된 class 속성의 값으로, DOM 객체 배열 리턴

```javascript
var dom = document.getElementsByClassName("class속성값");
```

#### (4) CSS 선택자에 알맞은, DOM 객체 리턴

```javascript
var dom = document.querySelector("CSS선택자"); // CSS선택자 앞에 꼭 #붙여주기
```

#### (5) CSS 선택자에 알맞은, DOM 객체 배열 리턴

```javascript
var dom = document.querySelectorAll("CSS선택자")
```



---



## DOM 객체의 내용 접근

#### (1) 컨텐트 내용 접근

```javascript
dom.innerHTML
dom.textContent
```

#### (2) 속성 접근

```javascript
dom.getAttribute('속성명')
```



---



## DOM  객체 편집

#### (1) 컨텐트 편집

* 태그와 텍스트 모두 수정하고 싶을 때

  ```javascript
  dom.innerHTML = "<p>새로운내용</p>";
  ```

* 텍스트만 수정하고 싶을 때

  ```javascript
  dom.textContent = "새로운내용";
  ```

#### (2) 스타일 편집

* 기본

  ```javascript
  dom.style.CSS속성명 = CSS속성값;
  ```

* CSS속성명

  * CSS의 속성명 그대로 사용
  * 단,  javascript는 `-`를 쓰지 않기 때문에,`-` 대신 바로 `다음 알파벳을 대문자`로 바꿔 사용
  * `background-color` 는 `backgroundColor` 로

* 예시

  ```javascript
  dom.style.color = "red";
  dom.style.backgroundColor = "yellow";
  ```

#### (3) 속성 편집

* 속성 추가

  ```javascript
  dom.setAttribute('속성명', '속성값');
  ```

* 속성 삭제

  ```javascript
  dom.removeAttribute('속성명');
  ```




---



## 이벤트 모델

> 자바스크립트는 이벤트 드리븐 모델에 기반하여 동작함.
>
> 이벤트에 따라 이벤트 핸들러를 호출하여 실행하는 모델

* 이벤트 (event)
  
  * 웹페이지 안에서 발생한 여러 가지 사건
* 이벤트 핸들러 (event handler)
  
* 이벤트에 따라 대응하는 처리
  
* 이벤트 타겟 (event target)

  * 이벤트가 일어날 객체

* 이벤트 타입 (event type)

  * 이벤트의 종류
  * click 같은거

  

### 자바스크립트가 지원하는 이벤트

> 1. 애플리케이션 사용자가 발생시키는 이벤트
> 2. 애플리케이션이 스스로 발생시키는 이벤트

* `load`

  * 문서의 모든 콘텐츠(images, script, css, etc) 가 로드된 후 브라우저에서 자동으로 발생하는 이벤트
  * 페이지 로드했을 때 자동으로 실행하고 싶은 이벤트 핸들러와 연결해 사용!

* `click`

  * 클릭한 위치의 (x, y) 좌표 정보를 가져오고 싶을 때

    ```html
    <h1>테스트</h1>
    </div>
    <script>
    function clickHandler() {
    	var dom = document.getElementsByTagName("h1")[0];
    	dom.addEventListener("click", displayAlert);
    }
    function displayAlert(e) {	
    	window.alert("클릭 : " + e.pageX + ", " + e.pageY);
    	window.alert("클릭 : " + e.screenX + ", " + e.screenY);
    	
    }
    window.addEventListener("load", clickHandler);
    </script>
    ```

* `mousedown`, `mousemove`, `mouseover`, `mouseup`

* `keydown`, `keypress`, `keyup`

* `change`, `reset`, `submit`

* `blur`, `focus`

* `setTimeout(function(){}, n초)` 

  * `n초` 후에 `function()` 실행 

  



### 이벤트 핸들러 등록하기

> DOM 객체에 이벤트를 연결하는 방법 
>
> 구현방법 3가지

#### (1) 인라인 이벤트 모델 (지역적) 

>  태그마다 속성으로 정의

```javascript
<태그명 [value="이벤트 핸들러에 전달하고 싶은 것"] on이벤트명 = "이벤트핸들러명([this])">
```

```javascript
<script>
	function 이벤트핸들러명([p]){
		// 연결한 이벤트 발생시 실행할 코드
	}
</script>
```

* 이벤트핸들러에 **전달하고 싶은 것**이 있으면,

  *  `value` 속성을 추가하여 **전달할 것**을 `value`속성값에 넣고,
  * 인자로 `this` 객체를 사용한다.
  * 이벤트 핸들러 매개변수는 `this`를 통해 이벤트를 발생시킨 객체를 받을 수 있다.
  * `value` 속성값은 `p.value` 를 통해 접근이 가능하다

* 이벤트 핸들러와 연결된 `DOM 객체` 접근 - 3가지 방법 

  * `p.속성`
  * `document.객체접근.속성`
  * `this.속성` (X)

* 예시

  ```javascript
  <button value="red" onclick="btn_onclick(this)">빨강색</button>
      <button value="blue" onclick="btn_onclick(this)">파랑색</button>
      <button value="green" onclick="btn_onclick(this)">녹&nbsp;&nbsp;색</button>
      <hr>
      <h2></h2>
  
      <script>
          var dom = document.getElementsByTagName("h2")[0];
          var date = new Date(); // 현재 날짜 및 시간
          dom.innerHTML = '오늘은 ' + date.getFullYear()+'년 ' + (date.getMonth()+1)+'월 ' + date.getDate()+'일입니다.';
          function btn_onclick(p){
              dom.style.color = p.value;
          }
      </script>
  ```

* 디폴트 이벤트 핸들러

  ```html
  <a href="URL" onClick="test(); return false;">디폴트 이벤트 핸들러</a>
  <script>
  	function test()
      {
          alert("인라인 이벤트 모델 버튼을 클릭하였습니다.");
      }
  </script>
  ```

  * 태그에 `return false` 를 추가해주면 `test()` 만 실행이 되고 URL로 이동하지 않는다.
  * 디폴트는 많이 사용하지 않지만 주로 `<a> 태그`에 사용

  

#### (2) 고전 이벤트 모델 (전역적)

> `<script>` 태그 안에 정의

```javascript
function 이벤트핸들러명([e]){
	// 이벤트 발생시 실행할 코드
}
dom.onclick = 이벤트핸들러명;
```

* 윈도우 객체에 이벤트 핸들러 추가

  ```javascript
  window.addEventListener("on이벤트명", 이벤트핸들러명);
  ```

* 이벤트 핸들러와 연결된 `DOM 객체` 접근 - 3가지 방법
  * `dom.속성`
  * `this.속성`
  * `e.target.속성`
  
* 등록된 이벤트 핸들러를 해제하려면, 핸들러를 등록한 속성의 값에 `null`을 재할당

* 디폴트 이벤트 핸들러

  ```html
  <a id="t" href="URL">디폴트 이벤트 핸들러</a>
  <script>
  	function test()
      {
          alert("고전 이벤트 모델 버튼을 클릭하였습니다.");
          return false;
      }
      var dom = document.querySelector("#t");
      dom.onclick = test;
  </script>
  ```

  * `test()` 함수 안에` return false` 추가해주면 함수만 실행 되고 URL로 이동하지 않는다.
  * 디폴트는 많이 사용하지 않지만 주로 `<a> 태그`에 사용

  

#### (3) 표준 이벤트 모델 (전역적)

> `<script>` 태그 안에 정의

```javascript
function 이벤트핸들러명([e]){
	// 이벤트 발생시 실행할 코드
}
dom.addEventListener("이벤트명", 이벤트핸들러명);
```

* 이벤트 핸들러 등록

  ```javascript
  dom.addEventListener("이벤트명", 이벤트핸들러명, [useCapture]);
  ```

* 이벤트 핸들러 해제

  ```javascript
  dom.removeEventListener("eventName", handler);
  ```

* window 객체에 이벤트 핸들러 추가

  ```javascript
  window.addEventListener("이벤트명", 이벤트핸들러명);
  ```

* 이벤트 핸들러와 연결된 `DOM 객체` 접근 - 3가지 방법

  * `dom.속성`
  * `this.속성`
  * `e.target.속성`
  
* 디폴트 이벤트 핸들러

  ```html
  <a id="t" href="URL">디폴트 이벤트 핸들러</a>
  <script>
  	function test()
      {
          e.preventDefault();
          alert("표준 이벤트 모델 버튼을 클릭하였습니다.");
      }
      var dom = document.getElementById("t");
      dom.addEventListener("click", test);
  </script>
  ```

  * `test()` 함수 안에` e.preventDefault` 추가해주면 함수만 실행 되고 URL로 이동하지 않는다.
  * 디폴트는 많이 사용하지 않지만 주로 `<a> 태그`에 사용

  

#### [고전 이벤트 모델] vs [표준 이벤트 모델]

* 고전
  * DOM 객체의 **한 이벤트**당 **한 개의 이벤트핸들러**
  * **여러 개의 핸들러 추가 안됨**
  * 이전에 연결한 것이 있어도 새로 연결된 이벤트핸들러만 실행됨
* 표준
  * DOM 객체의 **한 이벤트**에 **여러 개의 이벤트핸들러** 추가 가능