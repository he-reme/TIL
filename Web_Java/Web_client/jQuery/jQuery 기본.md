# jQuery 기본

* 크로스 플랫폼을 지원하는 경량 javascript library
* HTML 문서의 탐색이나 조작, 이벤트 핸들링, 애니메이션, Ajax 등을 멀티 브라우저를 지원하는 API를 통해 간편하게 사용
* 2019년도 기준 상위 100만개의 웹페이지 중 84%가 jQuery 사용
  * 신규 프로젝트는 거의 Vue로 만들어지고 있음

<br>

#### 특징

* 크로스 플랫폼을 지원하는 jQuery는 어떠한 브라우저에서도 동일하게 동작
* 브라우저 호환성을 고려하여 대체 코드를 작성할 필요 없음
* **네이티브 DOM API를 보다 직관적이고 편리한 API를 제공하여 개발 속도를 향상시킴**
* Event 처리, Ajax, Animation 효과를 쉽게 사용
* 다양한 Effect 함수를 제공하여 동적인 페이지 쉽게 구현

<br>

#### 주요 기능

* DOM 탐색과 조작
* 이벤트 바인딩과 처리
* Ajax 프로그래밍
* ㄴ다양한 Effect 제공

<br>

#### 사용

* CDN 버전
* [jQuery API](http://api.jquery.com) 혹은 W3 확인~

<br>

---

<br>

## 기본 구문

* Selector을 사용하여 DOM 객체 탐색하고, 반환된 레퍼세트를 통해 함수를 수행함
  * 레퍼세트
    * DOM 객체를 담음
    * `$(selector)` 가 탐색한 DOM 객체들
* Selector 표현식과 Action 메소드를 조합한 형태로 구문을 작성함
* jQuery로 DOM 을 탐색하기 전에, 웹 브라우저에 문서가 모두 로드되어 있어야 함
* jQuery는 Document Ready 이후 처리할 수 있는 두 가지 방법을 제공함

<br>

#### 기본 구문

`$(selector).action();`

* `$(selector)`
  * 탐색한 DOM객체들을 담은 래퍼세트를 반환
* 액션 함수 호출
  * 레퍼세트 객체를 통해 기능을 처리
  * 체이닝 가능
    * `$(selector).action1().action2();`

<br>

#### Document Ready

```javascript
$(document).ready(function() {
	// TODO
});
```

```javascript
$(function(){
	// TODO
});
```

