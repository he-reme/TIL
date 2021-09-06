# DOM 요소 선택

> Selector

* CSS에서 사용하는 Selector 표현 방식 사용
* 브라우저가 표준 CSS 선택자를 올바르게 구현하지 않았더라도, jQuery는 W3C 표준에 맞게 요소를 탐색
* DOM 탐색 결과로 래퍼세트라는 DOM을 래핑한 객체를 반환

<br>

---

<br>

## 선택자

> Selector

#### Selector을 이용한 DOM Element 검색

* CSS 문법을 확장하여 태그를 찾는 selector 제공
* 특정 브라우저에 의존적인 스크립팅을 벗어 날 수 있음

<br>

#### jQuery function의 기본 형식

`$("h1").css("color", "blue");`

* `$` : jQuery
* `("h1")` : selector
* `css("color", "blue")` : function

<br>

#### 요소 선택자

* Dom 객체를 탐색하여 래퍼세트 객체로 반환
* 종류
  * All selector
    * `$("*")`
    * HTML page에 있는 모든 문서 객체 선택
  * ID selector
    * `$("#id")`
    * `$("tagname#id")`
    * 선택자 중 사용 빈도 높음
    * DOM 객체를 가장 빨리 탐색함
  * Element selector
    * `$("elementName")`
  * Class selector
    * `$(".className")`
    * `$("tagname.className")`
    * 복합 선택자 (AND)
      * `$(".cn1.cn2")`
  * Multiple selector
    * `$("selector1, selector2, elector3, ...")`

<br>

---

<br>

## 계층 구조 탐색

#### Child selector

* `%("parent > child")`

* 부모 요소 바로 아래 자식

* 자식 선택자로, 바로 인접한 하위 자식들을 탐색
* 상하관계

<br>

#### Descendant selector

* `$("ancestor descendant")`
* 조상과 일치하는 요소에 포함된 모든 후손
* 자손 선택자로, 모든 하위 자식들을 탐색
* 상하관계

<br>

#### Next Adjacent selector

* `$("prevois + next")`
* Previous 요소 바로 다음에 나오는 형제수준의 next 요소

* 인접 선택자로, 인접한 바로 다음 형제를 탐색
* 평행관계

<br>

#### Next Siblings selector

* `$("previous ~ siblings")`
* Previous 요소 이후에 형제 요소 중 siblings와 동일한 모든 요소

* 평행관계

<br>

---

<br>

## 속성 탐색

#### 속성 선택자

* 이를 사용하여 DOM 요소가 가진 속성 값으로 DOM 객체를 탐색

* 표현식
  * `$(selector[attr])`
* 기본 선택자는 선택사항
  * 생략시, 모든 요소에 대해 주어진 속성 선택자를 비교

* 입력 양식과 관련된 요소를 선택할 때 사용

<br>

#### 형식

* `$(selector[attr])`
  * attr을 속성값으로 가지는 문서객체 선택
* `$(selector[attr = "value"])`
  * attr의 속성값이 value와 같은 문서객체 선택
* `$(selector[attr != "value"])`
  * attr의 속성값이 value와 같지 않은 문서객체 선택
* `$(selector[attr ~= "value"])`
  * attr의 속성값이 공백과 함께 value를 포함하는 문서객체 선택
  * 단어 단위로 찾음!!
    * man을 찾는다면 
      * `superman` : X
      * `super man` : O
* `$(selector[attr ^= "value"])`
  * attr의 속성값이 value로 시작하는 문서객체 선택
* `$(selector[attr $= "value"])`
  * attr의 속성값이 value로 끝나는 문서객체 선택
* `$(selector[attr *= "value"])`
  * attr의 속성값이 value를 포함하는 문서객체 선택
  * 문장속 value가 포함되어있기만 하면!
    * man을 찾는다면
      * `superman` : O
      * `super man` : O
