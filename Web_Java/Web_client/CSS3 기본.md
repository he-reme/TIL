# CSS3 기본

> CSS : Cascading Style Sheets

#### CSS?

* 스타일 사용 이유
  * 웹 문서의 내용과 상관없이 디자인만 바꿀 수 있음
  * 다양한 기기에 맞게 탄력적으로 바뀌는 문서를 만들 수 있음
* 웹 페이지를 표현하기 위해 스타일 규칙을 모아 놓은 문서

<br>

#### CSS 규칙

* **선택자(selector)** + **선언(declaration)** : 두 부분으로 구성됨

* 선택자

  * 규칙이 적용되는 엘리먼트

* 선언

  * 선택자에 적용될 스타일을 작성
  * 속성과 값으로 이루어짐

  ```css
  선택자 {
  	속성1 : 값1;
  	속성2 : 값2;
  }
  ```
  * 속성
    * 선택자에서 바꾸고 싶은 요소
    * color, font, width, height, border, ...
  * 값
    * 속성에 적용할 값
  * 여러 선택자에 동일한 스타일을 적용할 때
    * `,`로 구분하여 나열 (선택자 그룹화)
  * 선언 안에 하나 이상의 속성을 작성할 수 있고, `;`로 구분함
  * 주석 : `/* 내용 */`

* 선택자

  * class : `.클래스명`
  * id : `#아이디명`

<br>

---

<br>

## 스타일 시트 적용

<br>

#### 외부 스타일 시트 적용 방법 (2가지)

1. `<link>`
   * `<link rel="stylesheet" type="text/css" href="../css/my.css">`
   * `<head>` 태그 안에 작성
   * 속성
     * `rel` : HTML 페이지와 링크된 파일간의 관계를 의미
     * `type` 
     * `href` : CSS file 경로

2. `@import`
   * 스타일 시트 중 최상단에 위치해야 함 (하나만 사용 가능)
   * 사용
     * `@import url("file path");`
     * `@import "file path";`
   * `<link>`와 달리 `<style>`의 media 속성을 통해 보여지는 미디어 타입을 설정

<br>

#### 내부 스타일 시트 적용

* `<style>` 
  * 위 태그를 사용하여 내부 스타일 시트 적용
  * 태그 내부에 CSS 규칙 작성
* 외부 스타일 시트보다 우선 적용됨
* `<head>` 태그 내부에 작성

<br>

#### 인라인 스타일 적용

* **개별 element 마다 스타일을 적용**하므로 유지보수에 용이하지 않다
* 스타일 적용 우선 순위
  * 인라인 스타일 > 내부 스타일 시트 > 외부 스타일
* `style` 속성을 사용하고 속성값으로 CSS 규칙 작성
* `h2 style="color:magenta;"> Inline Style Sheet </h2>`

<br>

---

<br>

## 선택자

>  HTML 문서에서 **CSS 규칙 적용 타겟**이 되는 다양한 종류의 CSS 선택자가 존재함

<br>

#### 일반 선택자

* **전체 선택자**
  * HTML 문서 내 모든 element 선택
  * 전체적인 글꼴이나 margin 정도 설정할 때 사용
  * `*{}`
* **타입 선택자**
  * 매칭되는 element 선택
  * 1개 이상의 **태그명을 이용**
    * `,` 로 구분
  * `h1, h2, h3 {}`
* **클래스 선택자**
  * class 속성 값과 매칭되는 element 선택
  * 클래스명 : 공백X, 기호나 숫자 시작X (`-`, `_`는 허용)
  * `.className {}`
* **ID 선택자**
  * id 속성 값과 매칭되는 element 선택
  * `#idName {}`
* **우선 순위**
  * 전체 선택자의 우선순위가 가장 낮다
  * 전체 선택자 < 타입 선택자 < 클래스 선택자 < ID 선택자

<br>

#### 복합 선택자

* **자식 선택자**
  * 직속 하위 element 선택
  * 딱 E1 태그 바로 아래 있는 E2 태그들만 (자식들)
  * `E1 > E2 {}`
* **하위 선택자**
  * 하위 모든 element 선택
  * E1 태그 아래 있는 E2 태그의 아래 있는 모든 태그들도 포함 (자손들)
  * `E1 E2 {}`
* **인접 형제 선택자**
  * 인접 형제(sibling) 관계인 element 선택
  * E1 태그 바로 뒤에 나오는 첫번째 E2 태그 (하위 X), 바로 뒤에 동등한 들여쓰기에 나오는 태그)
  * `E1 + E2 {}`
* **일반 형제 선택자**
  * 형제(sibling) 관계인 element 선택
  * E1 태그 뒤에 나오는 들여쓰기가 동등한 모든 E2 태그들
  * `E1 ~ E2 {}`

<br>

#### + 그 외

#### 가상 클래스 선택자

* User Agent가 제공하는 가상의 클래스를 지정
* `가상 클래스 {}`
* 선택자
  * `:link` 
    * 방문하지 않은 링크 선택
    * `a` 태그에서 많이 사용됨
  * `:visited`
    * 방문한 링크 선택
    * `a` 태그에서 많이 사용됨
  * `:hover`
    * 지정된 요소에 마우스가 올라간 경우 선택
    * `a` 태그에서 많이 사용됨
  * `:active`
    * 지정된 요소가 활성화 된 경우 선택
    * `a` 태그에서 많이 사용됨
  * `:focus`
    * 지정된 요소가 포커스를 가질 경우 선택
  * `:first-child`
    * 지정된 요소 중 부모의 첫 번째 자식 선택
  * `:last-child`
    * 지정된 요소 중 부모의 마지막 자식 선택
  * `nth-child(n)`
    * 지정된 요소 중 n번째 자식 선택 (n = 0, 1, ...)
      * 자식 순번은 1부터 시작. 0은 본인
    * `2n` , `2n+1` : 짝수, 홀수 선택 (수열 선택 가능)
  * `:enabled`
    * 지정된 요소가 enabled인 경우 선택
  * `:disable`
    * 지정된 요소가 disabled인 경우 선택
  * `:checked`
    * 지정된 요소가 checked인 경우 선택

<br>

#### 가상 엘리먼트 선택자

* 보이지 않는 가상의 엘리먼트 선택
* `::가상 엘리먼트 {}`
* 선택자
  * `::after`
    * 지정된 요소 뒤에 content 추가
  * `::before`
    * 지정된 요소 앞에 content 추가
  * `::first-letter`
    * 지정된 요소의 **첫 번째 문자** 선택
  * `::first-line`
    * 지정된 요소의 **첫 번째 라인** 선택
  * `::selection`
    * 사용자에 의해 선택된 요소(마우스 드래그)의 위치 선택

<br>

#### 속성 선택자

* 특정한 속성을 가지거나 속성 값을 갖는 엘리먼트 선택
* 속성 선택자를 사용하기 위해서는 HTML 문서를 작성할 때 `name`, `title`등의 속성값을 규칙적으로 정의해야 함
* 화면에 같은 분류의 많은 항목들을 일괄적으로 선택할 때 유용
  * 예) 특정 이름을 갖는 체크박스
* 선택자
  * `[A]`
    * A 속성이 포함된 엘리먼트 선택
  * `[A=V]`
    * A 속성 값이 V와 정확히 일치하는 엘리먼트 선택
  * `[A~=V]`
    * A 속성 값이 V 단어를 포함하는 엘리먼트 선택
    * V 단어 : word, space로 구분됨
  * `[A^=V]`
    * A 속성 값이 V로 시작하는 엘리먼트 선택
  * `[A*=V]`
    * A 속성 값이 V를 포함하는 엘리먼트 선택
    * V : 단어가 아니어도 됨
  * `[A$=V]`
    * A 속성 값이 V로 끝나는 엘리먼트 선택
  * `[A|=V]`
    * A 속성 값이 정확히 V이거나, V-로 시작하는 엘리먼트 선택
    * `V-` : 하이픈이 붙은 엘리먼트

<br>

#### CSS 규칙 적용 우선순위

* 같은 엘리먼트에 두 개 이상의 CSS 규칙이 적용된 경우되었을 때 우선 적용되는 경우
  * 마지막 규칙
    * CSS 규칙들 중 하단에 작성한 규칙
  * 구체적인 규칙
    * `p {}` 보다는 `p b {}`가 더 구체적이므로 `p b {}`가 적용됨
  * !important
    * 속성 값 뒤에 `!important`를 작성하면, 같은 엘리먼트에 대해 보다 우선적으로 스타일 적용됨

<br>

---

<br>

## Font 속성

<br>

#### 개요

* `<font>` tag 관련 속성은 CSS property로 대체 가능하므로 추천하지 않는 기능
* CSS Font 관련 속성은 text의 글꼴, 굵기, 크기, 스타일 등을 지정
* `font-family`, `font-size`, `font-style`, `font-variant`, `font-weight`, `font`로 구성
  * `font-family` : `E{font-family : 글꼴이름1, 글꼴이름2, ...}`
* CSS Parser는 앞의 글꼴부터 읽음
  * 글꼴이 사용자 PC에 없는 경우, 다음 글꼴을 적용
* generic font명을 뒤에 작성하는 것이 일반적
* font name에 white-space가 포함된 경우 `""` (quotation)으로 감싸야 함
  * `E{font-family : monospace, "Times New Roman";}`

<br>

---

<br>

## Text 속성

<br>

#### 개요

* CSS Text 관련 속성
  * 글자, 공간, 단어, 문단들이 보여지는 속성을 정의

* 들여쓰기를 위해 `&nbsp;` 문자를 사용하는 것이 아니라, `text-indent` 속성을 사용하여 들여쓰기를 적용

<br>

#### 속성

* `text-align`
  * text 정렬 방식 지정
* `text-decoration`
  * text 장식 지정
  * `none` , `underline`, `overline`, `line-through`, `blink`
* `color`
  * text 색상 지정
* `text-ident`
* `text-transform`
* `white-space`
* `vertical-align`
* `letter-spacing`
* `word-spacing`
* `line-height`

<br>

---

<br>

## 사용자 인터페이스 속성

<br>

#### 개요

* 화면에 출력될 엘리먼트들에 디자인 요소를 추가하는 속성
* 커서의 모양이나 리스트 형태를 변경
* 문서의 배경색과 배경 이미지를 변경
* 엘리먼트가 화면에 출력되는 방식을 조정

<br>

#### 속성

* `cursor`
  * 사용자 환경의 마우스 모양을 변경
* `classification`
  * 리스트 글머리 기호를 변경
* `display`
  * 엘리먼트가 화면에 출력되는 방식을 조정
* `background-color`
  * 배경색을 지정
* `background`
  * 배경 관련 속성을 한번에 지정
  * font 속성과 달리 속성 값 순서에 구애 받지 않음

* `background-image`
  * 배경을 이미지로 지정
* `background-attachment`
* `background-repeat`
* `background-position`

<br>

---

<br>

## 테이블 & 테두리 속성

<br>

#### 개요

* `<table>` 태그 관련 속성
  * 테이블의 너비나 높이를 지정하고, cell 내부 내용을 정렬
* 테두리 관련 속성
  * 테두리 모델을 설정하여, 테두리 스타일과 너비 등을 지정

<br>

#### 테이블 관련 속성

* `table-layout`
* `width`
  * 테이블 너비 설정
* `height`
  * 테이블 높이 설정
* `text-align`
  * cell 내부 내용을 수평 정렬
* `vertical-align`
  * cell 내부 내용을 수직 정렬

<br>

#### 테두리 관련 속성

* `border-collapse`
  * 분리된 테두리 모델, 통합된 테두리 모델을 설정
* `border-style`
  * 테두리 스타일 설정
* `border-width`
  * 엘리먼트의 4개 테두리 너비 설정
* `border-color`
  * 엘리먼트의 테두리 색 설정
* `border`
  * 테두리 관련 속성을 한번에 지정하는 단축형 속성

<br>

---

<br>

## 박스 모델

#### 개요

* CSS는 모든 엘리먼트가 여러 겹의 상자로 둘러 쌓여 있다고 가정함
* 구분 (순서대로 컨텐츠에서 멀어지는 부분..)
  * 컨텐츠 (Content)
  * 패딩 (Padding)
  * 테두리 (Border)
  * 마진 (Margin)
* 컨텐츠 정렬 또는 위치 지정
  * Pading, Margin 속성 활용
* 박스 모델을 활용하여 다양한 형태의 테이블이나 버튼을 직접 작성하여 활용

<br>

#### margin

* Box의 마진 영역 너비를 지정
* 단위 `em`, `px`
* 값이 n개일 때
  * 1 : 모든 면에 적용
  * 2 : 1번째는 `{top, bottom}` / 2번째는 `{right, left}`에 적용됨
  * 3 : 1번째는 `{top}` / 2번째는 `{right, left}` / 3번째는 `{bottom}`에 적용됨
  * 4 : `{top, right, bottom, left}` 순으로 적용됨

* CSS2.0부터 : 인접한 두 개 이상의 박스들의 인접 마진이 통합되어 단일 마진을 형성함
  * 두 개 이상의 인접 수직 마진은 통합
  * 두 개 이상의 인접 수평 마진은 통합X
  * 유동된 박스(floated)와 다른 박스의 수직 마진은 통합X
  * 위치(position) 값이 `absolute`와 `relative`로 위치된 박스의 마진들은 통합 X

<br>

#### padding

* Box의 패딩 영역 너비를 지정
* 값이 n개일 때
  * 1 : 모든 면에 적용
  * 2 : 1번째는 `{top, bottom}` / 2번째는 `{right, left}`에 적용됨
  * 3 : 1번째는 `{top}` / 2번째는 `{right, left}` / 3번째는 `{bottom}`에 적용됨
  * 4 : `{top, right, bottom, left}` 순으로 적용됨

<br>

#### 가운데 정렬

* `margin` 속성 사용

* 컨텐츠를 브라우저 화면의 가운데에 정렬되도록 설정 가능
* `E {margin : 0 auto}`
  * 첫 번째 값 - 상, 하 여백
  * 두 번째 값 - 좌, 우 여백
  * 속성값 `auto`
    * 현재 엘리먼트를 중심으로 상, 하 또는 좌, 우의 여백을 균등하게 분배
    * 가운데 정렬 효과

<br>

#### 100% 높이를 유지하는 레이아웃

* `min-height` 속성
  * 엘리먼트의 최소 높이를 보장하기 위해 사용
* `height`, `min-height` 속성을 같이 사용하면
  * 레이아웃의 높이를 100%로 유지 가능
* `<html><body>` 엘리먼트 하위에 100% 높이를 유지하는 `<div>` 엘리먼트 사용
* 브라우저 화면 크기를 늘리더라도 컨텐츠는 항상 브라우저의 100% 높이를 유지

```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8">
	<title>100% 높이를 유지하는 레이아웃</title>
	
	<style type="text/css">
		html, body { height: 100%; margin: 0; padding: 0; }
		#head { height: 100px; background: orange; position: relative; }
		#body { min-height: 100%; margin: -100px 0 -50px; }
		#content-area { padding: 100px 0 50px; height: 300px; }
		#foot { height: 50px; background: steelblue; }
	</style>
</head>
<body>
	<div id="head">head(height: 100px; position: relative;)</div>
	<div id="body"><div id="content-area">content(padding: 100px 0 50px; height: 300px;)</div></div>
	<div id="foot">foot(height: 50px;)</div>
</body>
</html>
```

<br>

---

<br>

## 포지셔닝

<br>

#### 개요

* 시각적인 측면에서 HTML의 가장 중요한 요소

* HTML 내 부분 문서의 위치를 지정하거나 객체의 보임/안보임을 다룸
* 엘리먼트 위치를 고정시키거나 브라우저의 크기에 따라 이동하는 등의 설정을 함
* 정적인 HTML을 JavaScript를 사용하여 동적으로 만들기 위한 가장 기본적인 속성

<br>

#### width, height

* length (길이 값)
  * `px`, `pt`, `cm`, `mm`, `in` 등의 길이 단위 사용
* 백분율 (%)
  * 상위 block에 대한 백분율 단위
  * 상위 block의 크기가 바뀌면 자신의 크기도 자동 변경됨
* `auto`
  * width의 경우 : `100%`, 자신의 상위 block이 허용하는 width 크기 만큼 채움
  * height의 경우 : `0%`, height를 결정하는 요인은 block box 속의 내용물의 크기

<br>

#### position

* `static`
  * 기본값
  * 일반적인 내용물의 흐름
  * top과 left에서의 거리를 지정할 수 없음
* `relative`
  * HTML 문서에서의 일반적인 내용물의 흐름
  * top, left 거리를 지정
* `absolute`
  * 자신의 상위 box 속에서의 top, left, right, bottom 등의 절대적인 위치를 지정
* `fixed`
  * 스크롤이 일어나도 항상 화면상의 지정된 위치에 있음

<br>

#### top, left, bottom, right

* 엘리먼트의 위치를 지정하기 위해 사용됨
* 자신이 포함되어 있는 박스 속에서의 top, left, bottom, right에서의 거리를 지정하는 속성
* `E { top: 길이값|백분율|auto }`
* 각 `<div>` 엘리먼트의 `position` 속성이 `absolute`로 설정되어있기 때문에 절대적인 위치 지정 가능

<br>

#### overflow

* 상위 엘리먼트에 속한 내용이 엘리먼트의 크기보다 클 경우 어떻게 처리할 것인지 설정
* 속성값
  * `visible`
    * 기본값, box 속의 내용을 모두 표시
    * 내용의 크기에 따라 box의 가로, 세로 폭이 늘어남
  * `hidden`
    * box의 width, height를 지정했을 경우, 지정된 범위를 넘치는 내용은 보이지 않음
  * `auto`
    * 지정된 범위를 넘치는 내용은 스크롤바를 이용하여 표시함

<br>

#### visibility

* 엘리먼트를 화면에 보이거나 숨기기 위해서 사용
* 속성값
  * visible : 화면에 표시
  * hidden : 화면에서 숨김
  * display : 화면에서 숨기고, 면적도 차지하지 않게 함