# Event

* 웹 페이지에서 여러 종류의 상호작용이 있을 때마다 이벤트 발생
* 다양한 종류의 이벤트 존재
  * 웹 페이지가 로딩되었을 때
  * 페이지를 스크롤 했을 때
  * 브라우저 창의 크기를 조절했을 때
  * 마우스를 클릭 했을 때
  * 키보드로 키를 입력 했을 때
  * Form이 Submit 되었을 때
  * Input의 내용이 변경 되었을 때
  * 마우스를 움직여서 Element를 이동할 때
* JavaScript를 사용하여 DOM에서 발생하는 이벤트를 감지하여 이벤트에 대응하는 여러 작업 수행
* 이벤트는 일반적으로 함수와 연결됨
  * 이 함수는 이벤트가 발생되기 전에는 실행되지 않다가 
  * 이벤트가 발생할 경우 실행
  * **이벤트 핸들러** 또는 **이벤트 리스너**라고 함
  * 이 함수에 이벤트 발생시 실행해야 하는 코드 작성

<br>

---

<br>

## 이벤트의 종류

#### 마우스 이벤트

* 가장 많이 사용하는 이벤트
* 마우스 이벤트 핸들러에 전달되는 이벤트 객체에는 정보를 담고 있음
  * 마우스 위치, 버튼 상태 등
* **이벤트**
  * `onclick` ★
    * 마우스로 Element를 클릭 했을 때 발생
  * `ondblclick`
    * 마우스로 Element를 더블 클릭 했을 때 발생
  * `onmouseup`
    * 마우스로 Element에서 마우스 버튼을 올렸을 때 발생
  * `onmousedown`
    * 마우스로 Element에서 마우스 버튼을 눌렀을 때 발생
  * `onmouseover`
    * 마우스를 움직여서 Element 밖에서 안으로 들어 올 때 발생
  * `onmouseout`
    * 마우스를 움직여서 Element 안에서 밖으로 나갈 때 발생
  * `onmousemove`
    * 마우스를 움직일 때 발생

<br>

#### 키보드 이벤트

* 키보드의 커서가 웹 브라우저에 나타나는 지점에서 키보드를 조작할 때 이벤트 발생
* 키보드 조작은 운영체제 영향을 받으므로 특정 키가 이벤트 핸들러에게 전달되지 않을 수 있음
* 키보드 커서가 나타내는 요소가 없다면 document에서 이벤트가 발생함
* **이벤트**
  * `onkeydown`
    * 키보드를 누르는 순간 발생
  * `onkeypress`
    * 키보드가 눌려 졌을 때 발생
    * 키를 눌렀다가 떼기 바로 직전!
  * `onkeyup`
    * 누르고 있던 키를 뗄 때 발생

<br>

#### Fraim(UI) 이벤트

* 특정 DOM 문서에 관련된 이벤트가 아니라 Frame 자체에 대한 이벤트
* Frame 이벤트 중에서는 **load 이벤트가 가장 많이 사용됨**
* load
  * 문서 및 자원들이 모드 웹 브라우저에 탑재되면 이벤트를 수행

* unload

  * 사용자가 브라우저를 떠날 때 이벤트가 발생하지만,
  * 사용자가 브라우저를 떠나는 것을 막을 수는 없음

* **이벤트**

  * `onload` ★
    * document, image, frame 등이 모두 로딩 되었을 때 발생

  * `onabort`
    * 이미지 등의 내용을 로딩하는 도중 취소 등으로 중단 되었을 때 발생
  * `onerror`
    * 이미지 등의 내용을 로딩 중 오류가 발생 했을 때 발생
  * `onresize`
    * document, element의 크기가 변경 되었을 경우 발생
  * `onscroll`
    * document, element가 스크롤 되었을 때 발생
  * `onselect`
    * 텍스트를 선택 했을 때 발생

<br>

#### 폼(Form) 이벤트

* 웹 초기부터 지원되어 여러 웹 브라우저에서 가장 안정적으로 동작하는 이벤트
* form이 전송될 때
  * submit 이벤트 발생
  * 자주 사용되는 이벤트
* Form을 초기화 할 때
  * reset 이벤트 발생
* **submit / reset 은 이벤트 핸들러에서 취소할 수 있음**
  * 유효성 검사 후 submit해야 하는 경우에!
* **이벤트**
  * `onsubmit`
    * form이 전송될 때 발생
  * `onreset`
    * 입력 form이 reset될 때 발생
  * `oninput`
    * input 또는 textarea의 값이 변경 되었을 때 발생
  * `onchange` ★
    * select box, checkbox, radio button의 상태가 변경 되었을 때 변경
  * `onfocus(focusin)`
    * input과 같은 요소에 입력 포커스가 들어 올 때 변경
  * `onblur(focusout)`
    * input과 같은 요소 등에서 입력 포커스가 다른 곳으로 이동할 때 발생
  * `onselect`
    * input, textarea에 입력 값 중 일부가 마우스 등으로 선택될 때(드래그) 발생

<br>

---

<br>

## 이벤트 핸들러

* 이벤트 핸들러를 등록하다
  * 어떤 이벤트를 처리할 작업을 등록하는 것

<br>

#### 인라인 이벤트 핸들러

* JavaScript 초기에 사용한 방식
* HTML 요소의 내부에 직접 이벤트 핸들러 등록
* HTML 코드를 JavaScript 코드가 침범한다는 문제가 있음

* 최근에는 사용하지 않음
  * 단, 기존의 코드에서 사용 되었기 때문에 알아 두어야 함
* 여러 개의 함수를 한번에 호출 가능 
  * `onclick="f1(); f2();"`

* 최근 관심 받고 있는 CBD 방식의 framework / library에서는 인라인 방식으로 이벤트 처리
  * CBD에서는 html, css, js를 view의 구성 요소로만 보기 때문!
  * CBD 방식의 framework / library
    * Angular / React / Vue.js
  * CBD : Component Based Development

<br>

#### 이벤트 핸들러 프로퍼티 방식

* JavaScript에서 이벤트 핸들러를 등록하는 방법

* **이벤트 대상이 되는 특정 DOM을 선택하고 이벤트 핸들러를 등록**

* 예시

  ```html
  <script type="text/javascript">
  
  	window.onload = function() {
  		document.getElementById("div1").onclick = function () {
  			alert('안녕하세요');
  		};
  	};
  
  </script>
  
  <div id="div1">클릭해보세요</div>
  ```

* 장점
  * HTML코드와 JavaScript 코드 분리 가능

* 단점

  * 이벤트 핸들러 프로퍼티에 하나의 이벤트 핸들러만을 바인딩 할 수 있다는 단점을 가짐

  * 마지막에 바인딩된 이벤트 핸들러만 실행됨

  * 예시

    ```html
    <button id="btn">클릭해보세요</button>
    <script type="text/javascript">
      
      const btn = document.querySelector('#btn');
      
      // 첫번째 바인딩된 이벤트 핸들러 ==> 실행되지 않는다.
      btn.onclick = function () {
        alert('안녕하세요!!');
      };
      // 두번째 바인딩된 이벤트 핸들러
      btn.onclick = function () {
        btn.style.color = 'purple';
        btn.style.fontSize = '30px';
        btn.style.fontWeight = 'bold';
      };
    </script>
    ```

<br>

#### addEventListener 메소드 방식

* `addEventListener(arg1, arg2 [, arg3])`
* 전달 인자
  * 첫 번째 : 이벤트 이름
  * 두 번째 : 이벤트 핸들러
  * 세 번째 : 캡쳐링 여부
* 첫 번째 전달 인자의 이벤트 이름에는 `on`을 제거한 이벤트 이름을 사용
* 주의점
  * Internet Explorer 9 이전 버전에서는 사용 불가
  * 대신 `attachEvent()` 사용해야 함.

* `addEventListener` 메소드를 이용하여 대상 DOM 요소에 이벤트를 바인딩하고 해당 이벤트가 발생했을 때 실행될 콜백 함수(이벤트 핸들러)를 지정

* 장점

  * 하나의 이벤트에 대해 하나 이상의 이벤트 핸들러 추가 가능
  * 캡처링과 버블링 지원
  * HTML 요소 뿐만 아니라 모든 DOM(HTML, XML, SVG)에 대해 동작

* 사용 방법 1

  ```javascript
  const btn = document.querySelector('#btn');
  
  function f1() {
  	alert('안녕하세요!!');
  }
  
  btn.addEventListener('click', f1);
  ```

* 사용 방법 2

  ```javascript
  const btn = document.querySelector('#btn');
  
  btn.addEventListener('click', function () {
  	alert('안녕하세요!!');
  });
  ```

<br>

* 예시

  ```html
  <button id="btn">클릭해보세요</button>
  
  <script type="text/javascript">
    const btn = document.querySelector('#btn');
    
    // 첫번째 바인딩된 이벤트 핸들러
    btn.addEventListener('click', function () {
      alert('안녕하세요!!');
    });
    
    // 두번째 바인딩된 이벤트 핸들러
    btn.addEventListener('click', function () {
      btn.style.color = 'purple';
      btn.style.fontSize = '30px';
      btn.style.fontWeight = 'bold';
    });
  </script>
  ```

  * 둘 다 실행됨

* 요소의 값 검사를 여러 개 해야 할 경우(공통 로직) 규칙이 바뀌게 되면 참조하고 있는 모든 곳의 소스를 바꿔야 함 - **인자값이 있는 이벤트 핸들러 다루는 방법**

  * 예시

    ```html
    <label>아이디 <input type="text" /></label>
    <div class="message"></div>
    
    <script>
    	const input = document.querySelector('input[type=text]');
        const msg = document.querySelector('.message');
    
        input.addEventListener('blur', function () {
        	if (input.value.length < 8) {
            	msg.innerHTML = '아이디는 8자 이상 입력해 주세요';
            } else {
            	msg.innerHTML = '';
            }
        });
    </script>
    ```

  * 해결

    * 규칙에 해당하는 값을 인자로 받는 함수를 외부에 빼기!

    * 공통 규칙에 해당하는 값을 상수로 만들고 checkVal(인자)의 함수를 선언한 뒤 callback 함수 호출

      * 두번째 매개변수의 함수를 직접 호출할 경우 이벤트 발생 시까지 대기하지 않고 바로 실행
      * 해결하기 위해 함수 호출이 아닌 함수 지정을 선택
      * 해결은 되지만 인자를 전달 할 수 없음

    * 그래서!!!! 최종!!!

      * 이벤트 핸들러 내부에서 함수를 호출하는 방식으로 인수 전달 해결

    * 완벽하지 않은 해결

      ```html
      <label>아이디 <input type="text" /></label>
      <div class="message"></div>
      
      <script>
      	const MIN_ID_LENGTH = 8;
      	const input = document.querySelector('input[type=text]');
      	const msg = document.querySelector('.message');
      
          function checkVal(len) {
          	if (input.value.length < len) {
              	msg.innerHTML = '값은 ' + len + '자 이상 입력해 주세요';
            	} else {
              	msg.innerHTML = '';
            	}
          }
      
          //   이벤트 발생 시까지 대기하지 않고 바로 실행된다.
          input.addEventListener('blur', checkVal(MIN_ID_LENGTH));
          
          //   이벤트 발생 시까지 대기한다. 문제는 인자값을 전달할 수 없다.
          input.addEventListener('blur', checkVal);
        </script>
      ```

    * **완벽한 해결**

      ```html
      <label>아이디 <input type="text" /></label>
      <div class="message"></div>
      
      <script>
      	const MIN_ID_LENGTH = 8;
          const input = document.querySelector('input[type=text]');
          const msg = document.querySelector('.message');
      
          function checkVal(len) {
          	if (input.value.length < len) {
              	msg.innerHTML = '값은 ' + len + '자 이상 입력해 주세요';
              } else {
              	msg.innerHTML = '';
              }
          }
      
          input.addEventListener('blur', function () {
           	// 이벤트 핸들러 내부에서 함수를 호출하면서 인수를 전달.
           	checkVal(MIN_ID_LENGTH);
          });
      </script>
      ```

<br>

---

<br>

## 캡쳐링과 버블링

#### 이벤트 캡쳐링

* 이벤트가 발생한 요소를 포함하는 부모 HTML로부터 이벤트 근원지인 자식요소까지 검사하는 것
* 이벤트 캡쳐링에서 캡쳐 속성의 이벤트 핸들러가 등록되어 있으면 수행

<br>

#### 이벤트 버블링

* 이벤트 발생 요소부터 요소를 포함하는 부모요소까지 올라가면서 이벤트를 검사하는 것

* 이벤트 버블링에서 버블속성의 이벤트 핸들러가 등록되어 있으면 수행

<br>

#### 캡쳐링과 버블링 지정하기

* 캡쳐링
  * addEventListener 메소드의 세번째 인자 값을 true로 두었을 때
* 버블링
  * addEventListener 메소드의 세번째 인자 값이 false로 두었을 때

```javascript
element.addEventListener('click', f1, true);
element.addEventListener('click', f1, false);
```

<br>

---

<br>

## 활용

* 하나의 DOM 엘리먼트에 복수의 이벤트 핸들러를 등록할 수 있음

