# HTML 기본

#### 개요

* 마크업 언어로 웹 문서를 작성하며, tag를 사용하여 문서의 구조 등을 기술하는 언어

* html
  * head
    * meta, title, style, ...
  * body
    * p, div, form, ...

<br>

#### HTLM5 웹 문서를 구성하는 3가지 요소

* **HTML**
  * 구조
  * 웹페이지 문서 담당
* **CSS**
  * 표현
  * 웹페이지 디자인 담당
* **JS**
  * 동작
  * 웹페이지 이벤트 담당

<br>

#### 주석

* HTML tag의 내용을 설명하기 위한 용도
* `<!-- 이부분은 주석입니다 -->`

---

<br>

## 기본

#### tag와 속성

* HTML 문서는 `tag`로 만들어짐
* 전체 구성은 `html`, `head`, `body tag`로 구성

* tag는 시작tag와 종료tag로 쌍을 이루거나 시작 tag만 존재하는 tag도 있다
* 시작tag `<tagname>`와 종료tag `</tagname>`는 `/`로 구분하며 중첩되지 않도록 한다

* 각각의 tag는 속성과 속성의 값이 존재

* 글로벌 속성
  * HTML tag중 어느 tag에나 넣어서 사용할 수 있는 속성
  * class
    * tag에 적용할 스타일의 이름을 지정
    * 중복이 됨
  * id
    * tag에 유일한 ID를 지정함
    * 자바스크립트에서 주로 사용
    * 중복이 안됨
  * dir
    * 내용의 텍스트 방향을 지정
    * 왼쪽 >> 오른쪽 (기본값, ltr)
    * 오른쪽 >> 왼쪽 (rtl)
    * `<p dir="rtl">` : 오른쪽 맞춤
  * style
    * 인라인 스타일을 적용하기 위해 사용
    * `<p style="color:red; text-align:center;"></p>`
  * title
    * tag에 추가 정보를 지정
    * tag에 마우스 포인터를 위치시킬 경우 title의 값 표시
* **VS Code에서** 
  * `! + enter` 하면 기본적인 구조 생성됨

<br>

---

<br>

#### Root 요소

* `<html>` tag는 HTML 문서 전체를 정의
* Head `<head></head>`와 Body `<body></body>` 로 구성

<br>

#### Head 요소

* `<head>` tag
  * 브라우저에게 HTML문서의 머리 부분임을 인식

* `<title>` `<meta>` `<style>` `<script>` `<link>` tag를 포함 가능
* `<title>` tag
  * 문서의 제목을 의미
  * 브라우저의 제목 표시줄에 tag 내용이 나타남
* `<title>` tag 이외의 다른 tag로 표현한 정보는 화면에 출력 X

<br>

#### Body 요소 - body

* 웹 브라우저에 보여질 문서의 내용을 작성
* `<head>` tag 다음에 위치하고 `<head>` 내부에 위치하는 tag와 `<html>`을 제외한 모든 tag
* id 속성을 이용하여 문서 내에서 tag를 유일하게 식별 가능
  * id 속성은 중복 X
* class 속성을 이용하여 여러 tag에 공통적인 특성(CSS)을 부여
  * class 속성은 중복 O

<br>

#### Body 요소 - heading

* 문단의 제목을 지정할 때 사용
* `<h1>` ~ `<h6>` : 숫자가 커질수록 글자가 작아짐
* `<section>` tag
  * 이용하면 같은 tag를 서로 다르게 표현
  * 이를 이용하여 구분하면 각 문단의 제목을 하나의 tag로 작성 가능
  * 계층 구조로 사용하면 상대적으로 글자가 작아짐

<br>

---

<br>

#### 특수 문자

* `&nbsp;`
  * 공백
* `&lt;`
  * `<`
* `&gt;`
  * `>`
* `&amp;`
  * `&`
* `&quot;`
  * `"`
* `&copy;`
  * Copyright `ⓒ`
* `&reg`
  * registered trademark

<br>

---

<br>

#### 포맷팅 요소

* 포맷팅 요소에는 화면에는 동일하게 출력되지만 각 요소가 가진 의미가 다른 것이 있다.
* 나중에 필요할 때 찾아보기

<br>

---

<br>

#### 목록형 요소 ★★★

* `<ul>`
  * 번호 없는 목록을 표시
  * 항목 앞에 심볼을 표시
* `<ol>`
  * 번호 있는 목록을 표시
  * 숫자, 알파벳, 로마숫자 등으로 표시
  * 속성 : type
    * 속성값
      * 1 : 숫자(기본값)
      * a : 영문 소문자
      * A : 영문 대문자
      * i : 로마숫자 소문자
      * l : 로마숫자 대문자
  * 속성 : start
    * 숫자 : 시작번호
    * 100이면... 100 101 102 이렇게 숫자가 붙음
  * 속성 : reversed
    * 역순으로
* `<li>`
  * 목록 항목 `<ul>`이나 `<ol>`tag 하위에서 사용

* `<dl>`

  * 용어 정의와 설명에 대한 내용을 목록화해서 표시
  * 목록

* `<dt>`

  * 용어 목록의 정의 부분을 나타냄
  * 제목

* `<dd>`

  * 용어 목록의 설명 부분을 나타냄
  * 상세설명

* 응용

  ```html
  <dl>
  	<dt>제목1</dt>
  		<dd>상세설명1</dd>
  	<dt>제목2</dt>
  		<dd>상세설명2</dd>
  </dl>
  ```

  ```html
  <ol>
  	<li> HTML / XML
  		<dl>
  			<dt>HTML</dt>
  				<dd>Hypertext Markup Language</dd>
  			<dt>XML</dt>
  				<dd>eXtensible Markup Language</dd>
  		</dl>
  	</li>
  </ol>
  ```

<br>

---

<br>

## Table

```
<table>
	<thead>
		<tr>
			<th>열이름1</th>
			<th>열이름2</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>data1</td>
			<td>data2</td>
		</tr>
</table>
```

<br>

#### HTML table 모델

* HTML table 모델은 데이터를 행과 열의 셀에 표시
* 테이블은 수치 데이터를 보여줄 때 사용하고, 디자인은 하지 않는게 좋음!!
  * 테이블은 한번에 로드해서 보여주기 때문에
  * 데이터 량이 많아지면 로딩이 느려짐!
* 행 그룹 요소를 사용하여 행들을 그룹화
  * `<thead>`, `<tbody>`, `<tfoot>`
* 열 그룹을 위한 추가적인 구조 정보를 제공하는 요소
  * `<colgroup>`, `<col>`
* table의 셀이 가질 수 있는 것
  * `<th>` : 머리글
  * `<td>` : 데이터

<br>

#### table 제목

* `<caption>` 태그
* 잘 사용하진 않음

```html
<table>
	<caption> 테이블 제목 </caption>
	...
</table>
```

<br>

#### 행(Row) 그룹 요소

* table 행 그룹 요소는 table의 행들을 머리글, 바닥글, 하나 이상의 본체 항목으로 그룹핑
* 생략을 해줘도 괜찮다..
  * `<th>`, `<td>` 사용해주면 어차피 구분이 되기 때문
* 행 그룹 요소
  * 머리글`<thead>`
  * 본체항목`<tbody>`
  * 바닥글`<tfoott>`
* 각 행 그룹은 최소 하나 이상의 `<tr>`을 가져야 함

<br>

#### 열(Column) 그룹 요소

* table 열 그룹 요소는 table 내에서 구조적인 분리를 가능하게 함

* 열 그룹 요소

  * `<colgroup>` 요소
    * 명시적인 열 그룹을 만듦
    * `span` 속성 : 열 그룹에서 열의 개수를 정의
  * `<col>` 요소
    * 열을 묶어 그룹핑함
    * `span` 속성 : `<col>`에 의해 묶여진 열의 개수를 말함

* 그러나 속성들은 이제 css로 작성!

* 예시

  ```html
  <table>
  	<colgroup>
  		<col span = "2" style="background-color: skyblue">
  		<col width="200">
  </table>
  ```
  * `<col span = "2" style="background-color: skyblue">`
    * 앞에서 열 2개의 백그라운드 색을 스카이블루로.

<br>

#### 테두리 (border) 속성

* `cellspacing`
  * table cell과 cell 사이의 공간을 의미
  * td 사이의 거리
* `cellpadding`
  * cell 외곽과 cell 컨텐츠 사이 공간을 의미
  * td 안에서 테두리와 데이터의 거리
* 그러나.. 테두리 스타일 관련 속성을 지원하지 않고, css 사용

<br>

#### 셀 병합

* `<td>` 요소에 셀 병합을 위한 두개의 속성이 있음
  * `colspan` 속성
    * 두 개 이상의 열을 하나로 합치기 위해 사용
  * `rowspan` 속성
    * 두 개 이상의 행을 하나로 합치기 위해 사용

* 예시

  ```html
  <table>
  <tr>
  	<td>1<td>
  	<td>2</td>
  </tr>
  <tr>
  	<td>3</td>
  	<td>4</td>
  </tr>
  </table>
  ```

  ```html
  <table>
  <tr>
  	<td rowspan="2" class="view">1<td>
  	<td>2</td>
  </tr>
  <tr>
  	<td>4</td>
  </tr>
  </table>
  ```

  ```html
  <table>
  <tr>
  	<td colspan="2" class="view">1<td>
  </tr>
  <tr>
  	<td>3</td>
  	<td>4</td>
  </tr>
  </table>
  ```

  ```html
  <table>
  <tr>
  	<td>1</td>
  	<td rowspan="2" class="view">2<td>
  </tr>
  <tr>
  	<td>3</td>
  </tr>
  </table>
  ```

<br>

---

<br>

## 이미지

```html
<img src="경로" title="이미지제목" width="300" height="200" alt="이미지가 안보이나요?">
```

#### img

* `<img>` tag
  * 이미지를 삽입하기 위해 사용
* `src` 속성
  * 이미지 경로를 지정하기 위해 사용
  * 상대경로, URL 모두 가능
  * 필수 속성
* `height`, `width` 속성
  * 이미지 사이즈를 지정하기 위해 사용

* `alt` 속성
  * 이미지를 표시할 수 없을 때 화면에 대신하여 보여질 텍스트를 지정

<br>

#### img 설명글

* `<figure>`
  * 설명 글을 붙여야 할 대상을 지정
* `<figcaption>`
  * 설명글이 필요한 대상은 `<figure>` 태그로 묶고 설명글은 `<figcaption>` 태그로 묶음
  * 설명글을 붙일 수 있는 대상
    * 이미지나 오디오, 비디오 같은 미디어파일
    * 텍스트 단락이나 표

* 예시

  ```html
  <figure>
  	<img src="../img/night.png" title="야경">
  	<figcaption>홍제의 야경입니다.</figcaption>
  </figure>
  ```

<br>

---

<br>

## 링크

#### Anchor

* `<a>` tag 사용

  * 하나의 문서에서 다른 문서로 연결하기 위해 사용

  * 하이퍼링크

* tag를 서로 중첩해서 사용할 수 없음

* `href` 속성

  * 하이퍼링크를 클릭했을 때 **이동할 문서의 URL**이나 문서의 책갈피를 지정

* `target` 속성

  * 하이퍼링크를 클릭했을 때 현재 윈도우 또는 새로운 윈도우에서 이동할지를 지정
  * 속성값
    * `_self` 
      * 기본값
      * 현재 윈도우에서 다른 문서로 이동
    * `_blank`
      * 새로운 윈도우 또는 탭에서 다른 문서로 이동 (브라우저 설정에 따름)
    * `_parent`
      * 프레임을 사용했을 때 링크 내용을 부모 프레임에 표시
    * `_top`
      * 프레임을 사용했을 때 프레임을 벗어나 링크 내용을 전체 화면으로 표시

* 예시

  ```html
  <a href="index.html" target="_self">홈화면</a>
  
  <a href="https://www.naver.com" target="_blank">네이버</a>
  ```

<br>

#### #anchor

* 같은 페이지 안에서 특정 요소를 클릭 시 그 위치로 한 번에 이동시킨다

* 북마크에 자주 이용

* 예시

  ```
  <a href = "#anchor name"> text or image <a>
  <tag id = "anchor name"> text or image </tag>
  ```

  * id 이름이 `anchor name`인 tag로 이동!!
  * #은 id를 가리킴

<br>

#### map

* 하나의 이미지에 여러 개의 link (Click 위치에 따라 서로 다른 link)
* `<map name="map name"><area><area> ... </map>`
* 이미지에 영역을 표시 할 때 `<area>` 사용
* area의 속성
  * href : 링크 경로
  * target : 링크표시대상
  * shape : 링크로 사용할 영역의 형태
* shape의 값
  * default, rect, circle, poly

* 예시

  ```html
  <img src = "../logo.png" usemap="#logo">
  <map name="logo">
  	<area shape="rect" coords="5,5,185,80" href="https://www.naver.com" target="_blank">
  	<area shape="rect" coords="190,5,345,80" href="https://www.google.com" target="_blank">
  ```

<br>

---

<br>

## 프레임 요소

#### iframe

* 화면의 일부분에 다른 문서를 포함
* `src` 속성은 포함시킬 외부 문서의 경로를 지정 (상대경로, URL 모두 가능)
* `height`, `width` 속성
  * 프레임 사이즈를 지정
* `name` 속성
  * 프레임의 이름을 지정

* 예시

  ```html
  <a href="java.html" target="javacontent"> java fundamental </a>
  <iframe src="java.html" name="javacontent" width="500" height="300"></iframe>
  ```

<br>

---

<br>

## form control 요소

#### 개요

* 사용자로부터 데이터를 입력 받아 서버에서 처리하기 위한 용도로 사용
* 사용자의 요청에 따라 서버는 HTML form을 전달 (회원가입양식, 검색양식 등)
* 사용자는 HTML form에 적절한 데이터를 입력한 후 서버로 전송
  * submit
* 서버는 사용자의 요청을 분석한 후 데이터를 등록하거나, 원하는 데이터를 조회하여 결과를 다시 반환

* 사용자가 입력하기 위한 control 요소들은 모두 `<form>` tag 하위에 위치해야 서버로 전송됨

<br>

#### 종류

* `<form>`
  * 사용자에게 입력 받을 항목을 정의
  * form tag 내부에 여러 개의 control 요소를 포함
* `<input>`
  * 텍스트 box, 체크 box, 라디오 버튼 등 사용자가 데이터를 입력할 수 있도록 함.
* `<textarea>`
  * 여러 줄의 문자를 입력할 수 있도록 함.
* `<button>`
  * 버튼을 표시
* `<select>`
  * select box(드롭다운, 콤보box)를 표시
  * `<optgroup>`
    * select box의 각 항목들을 그룹화 함.
  * `<option>`
    * select box의 각 항목들을 정의 함.
* `<label>`
  * 마우스를 이용하여 `<input>` 항목을 선택 시 편리함을 제공.
  * `for` 속성을 이용하여 다른 control 요소와 텍스트를 연결시켜서 더 편리하게 선택할 수 있도록 함.
* `<fieldset>`
  * 입력 항목들을 그룹화 함.

* `<legend>`
  * `<fieldset>`의 제목을 지정 함.

<br>

---

<br>

## form

* 사용자가 입력한 자료들을 어떤 방식으로 서버로 전달할 것인지 결정

* 서버에서 어떤 프로그램을 이용해 처리할 것인지 결정
* `<form [속성="속성값"]> form control </form>`
* 속성
  * `method`
    * 사용자가 입력한 내용을 서버 쪽 프로그램으로 어떻게 넘겨줄지 지정
    * 속성값
      * `GET`
        * URL에 사용자가 입력한 내용이 표시됨
        * 256 ~ 2048bytes의 데이터만 서버로 전송됨
      * `POST`
        * URL에 사용자가 입력한 내용이 표시되지 않음
        * 사용자의 입력을 표준 입력으로 넘겨주기 때문에 입력 내용의 길이에 제한이 없음
  * `name`
    * form의 이름을 지정
    * 한 문서 안에 여러 개의 `<form>`태그가 있을 경우 구분자로 사용
  * `action`
    * `<form>`태그 안의 내용들을 처리해 줄 서버상의 프로그램 지정 (URL)
  * `target`
    * `<action>` 태그에서 지정한 스크립트 파일을 현재 창이 아닌 다른 위치에 열도록 지정
  * `autocomplete`
    * 자동완성 기능
    * 기본값 : on

<br>

#### label

* form control에 레이블(텍스트)를 연결

* 사용법

  * `<label [속성="속성값"]> 레이블 <input....> </label>`
  * `<label for="id이름"> <input id="id이름" [속성="속성값"]> </label>`

* 예시

  ```html
  <form method="POST" action="login.jsp">
  <ul type="none">
  	<li>
  		<label for="userid"> 아이디: </label>
  		<input type="text" id="userid" name="userid">
  	</li>
  	<li>
  		<label for="pass"> 비밀번호: </label>
  		<input type="text" id="pass" name="pass">
  	</li>
  	<li><input type="submit" value="로그인"></li>
  </ul>
  </form>
  ```

<br>

#### fieldset, legend

* form 요소를 그룹으로 묶음

* 예시

  ```html
  <fieldset>
  	<legend> 필수 입력 </legend>
      <ul type="none">
         <li>
  			<label for="userid"> 아이디: </label>
  			<input type="text" id="userid" name="userid">
  		</li>
          <li>
  			<label for="pass"> 비밀번호: </label>
  			<input type="text" id="pass" name="pass">
  		</li>
      </ul>
  </fieldset>
  <fieldset>
      <legend> 선택 입력 </legend>
      <ul type="none">
         <li>
  			<label for="phone"> 전화번호: </label>
  			<input type="text" id="phone" name="phone">
  		</li>
          <li>
  			<label for="address"> 주소: </label>
  			<input type="text" id="address" name="address">
  		</li>
      </ul>
  </fieldset>
  ```

<br>

---

<br>

## input

> form 태그 안에 input 태그 작성

#### 개요

* `<input>` tag는 type 속성에 따라 여러 가지 형태로 화면에 표시
* `<input type="유형" [속성="속성값"]`
* id 속성
  * 여러 번 사용된 폼 요소를 구분하기 위해 사용
  * id 속성값은 최소한 한 개 이상의 문자여야 함. 공백 허용X
* id & name
  * 같은 html document에서 id는 하나의 값만 가능
  * name은 중복 허용

<br>

#### type 속성(유형)

* text
  * 한 줄의 텍스트를 입력할 수 있는 텍스트 상자
* password
  * 비밀번호를 입력할 수 잆는 필드
  * text가 `*`로 표시됨
* search
  * 검색 상자
  * 박스 오른쪽에 `X`가 있어 텍스트를 쉽게 지울 수 있음

* tel
  * 전화번호를 입력할 수 있는 필드
* url
  * URL 주소를 입력할 수 있는 필드
* email
  * 메일 주소를 입력할 수 있는 필드
* datetime
  * 국제 표준시(UTC)로 설정된 날짜와 시간
  * 년, 월, 일, 시, 분, 초, 분할 초
* datetime-local
  * 사용자 지역을 기준으로 날짜와 시간
  * 년, 월, 일, 시, 분, 초, 분할 초
* date
  * 사용자 지역을 기준으로 날짜
  * 년, 월, 일

* number
  * 숫자를 조절할 수 있는 화살표
* range
  * 숫자를 조절할 수 있는 슬라이드 막대
  * min, max, value(페이지 로딩 시 초기값)
* color
  * 색상표
  * 지원 브라우저 : 파이어폭스, 크롬, 오페라와 안드로이드 브라우저
    * 그 외는 텍스트 필드로 표시
* checkbox
  * 주어진 항목에서 2개 이상 선택 가능한 체크박스
  * 다중선택
  * `value` 속성을 주어 값을 설정해줘야 함
  * `<label>` 태그로 묶어주면 체크박스 말고 텍스트 클릭해도 클릭됨
    * `<label for="game"><input type="checkbox" name="hooby" id="game" value="게임"> 게임 </label>`
* radio
  * 주어진 항목에서 1개만 선택할 수 있는 라디오 버튼
  * `name`속성의 값이 모두 일치해야 같은 그룹으로 인식함
  * `value` 속성을 주어 값을 설정해줘야 함
  * 단일 선택
* file
  * 파일을 첨부할 수 있는 버튼
* hidden
  * 사용자에게 보이지 않지만 서버로 넘겨지는 값을 설정

<br>

#### type 속성(유형) - 버튼

* `<input type="submit | reset | button" [value="버튼라벨"] [속성="속성값"]>`

* button
  * 자체 기능은 없는 버튼
  * 스크립트 함수와 연결해 사용
    * `onclick` 속성 사용
    * `onclick="checkValid();"`
* submit
  * 사용자가 입력한 form의 정보를 서버로 전송하는 버튼
* reset
  * `<input>` 요소에 입력한 모든 정보를 초기화하는 버튼
* image
  * submit + image 버튼
  * `<input type="image" src="img path" alt="대체텍스트" [속성="속성값"]>`

<br>

#### 속성

* autofocus
  * 페이지를 불러 오자마자 폼의 요소 중에서 원하는 요소에 마우스 커서를 표시
* placeholder
  * 텍스트를 입력할 때 도움이 되도록 입력란에 적당한 힌트 내용 표시
  * 클릭 시 자동으로 내용이 사라짐
* readonly
  * 입력란에 텍스트를 사용자가 직접 입력하지 못하게 읽기 전용으로 지정
  * `readonly`, `readonly="readonly"`, `readonly="true"`로 표현
* required
  * form에 data를 입력한 후 submit 클릭 시 data를 서버로 전송하기전 필수 입력 항목을 체크
  * `required`, `required="required"`로 표현
* min, max, step
  * step : 일정 간격 지정
* size, minlength, maxlength
  * size : 화면에 보여지는 글자의 길이 지정
  * minlength, maxlength : 텍스트 입력시 최대, 최소길이 지정
* height, width
  * image의 너비와 높이 지정
* list
  * `<datalist>`에 미리 정의해 놓은 옵션 값을 `<input>` 안에 나열해 보여줌
* multiple
  * type이 `email`, `file`인 경우 두 개 이상의 값을 입력하게 해줌
  * `<input>` 태그 안에 속성 이름만 표시하면 됨

<br>

---

<br>

## 여러 data 나열

#### dropdown

* 사용자 입력이 아닌 여러 옵션 중에서 선택하는 목록

* `<select>` 태그

  * select box (dropdown) 를 표시
  * 속성
    * `size` : 화면에 표시될 dropdown 메뉴의 항목 개수 지정
    * `multiple` : 브라우저 화면에 여러 개의 옵션이 함께 표시되면서 ctrl 키를 누른 상태로 여러 항목을 선택 (다중선택)

* `<option>` 태그

  * select box에 포함될 항목들을 정의
  * 속성
    * `value` : 옵션을 선택했을 때 서버로 넘겨질 값을 지정
    * `selected` : 화면에 표시될 때 기본으로 선택되어 있는 옵션을 지정

* 예시

  ```html
  <select name="area">
      <option value="010" selected="selected"> 핸드폰 </option>
      <option value="02"> 서울 </option>
      <option value="031"> 경기도 </option>
      <option value="041"> 충청도 </option>
      <option value="051"> 경상도 </option>
      <option value="061"> 전라도 </option>
  </select>   
  ```

* `<optgroup>`

  * dropdown 목록에서 여러 항목들을 몇 가지 그룹으로 묶을 경우

  * `label` 속성을 이용하여 그룹의 제목을 지정

  * 예시

    ```html
    <label for="chanel"> 선호채널 </label>
    <select id="chanel" name="chanel">
        <optgroup label="지상파">
        	<option value="mbc"> MBC </option>
            <option value="kbs" selected="selected"> KBS </option>
        	<option value="sbs"> SBS </option>
        </optgroup>
        <optgroup label="종합편성채널">
        	<option value="jtbc"> JTBC </option>
            <option value="tvn"> TVN </option>
            <option value="ytn"> YTN </option>
        </optgroup>
    </select>
    ```

<br>

#### datalist

* `<input>`과 함께 사용

* 텍스트필드에 직접 값을 입력하는 것이 아닌 datalist의 선택 값이 텍스트 필드에 입력됨

* ```html
  <input type="text" list="datalist_id">
  <datalist id="datalist_id">
  	<option>...</option>
      <option>...</option>
      ...
  </datalist>
  ```

* `<option>` 속성

  * `value` : 사용자가 레이블을 선택했을 때 서버로 넘겨질 값 지정
  * `label` : 사용자를 위해 브라우저에 표시할 레이블. 따로 지정하지 않을 경우, value값을 레이블로 사용

* 예시

  ```html
  <label for="bbteam"> 응원팀 </label>
  <input type="text" id="bbteam" list="teamlist">
  <datalist id = "teamlist">
  	<option value="bears" label="두산베어스"></option>
      <option value="tigers" label="KIA타이거즈"></option>
      <option value="dinos" label="NC다이노스"></option>
      ...
  </datalist>
  ```

<br>

---

<br>

## 기타 form control

#### button

* `<button>`태그
  * type 속성은 버튼이 활성화 되었을 때 어떤 동작을 할지 지정
  * 기본은 `submit` 
    * `<form>` 태그 내에 사용한다면
* `<button [type="submit|reset|button"]> 내용 </button>`
* `<input>` VS `<button>` 
  * contents를 포함할 수 있음
  * 아이콘 추가, CSS를 이용하여 원하는 형태로 꾸밀 수 있음

<br>

#### progress

* 작업의 진행 상태를 표시

* `<progress value="값" [max="값"]></progress>`
  * 작업의 시작을 0, 최종 완료를 최대값으로 지정
* 속성
  * `value`
    * 작업 진행 상태를 나타냄
    * 부동 소수점으로 표현
    * 0보다 크거나 같고 max보다는 작거나 같아야 함
    * max defult 값 : 1.0
  * `max`
    * 작업이 완료되려면 얼마나 많은 작업을 해야 하는지 부동 소수점으로 표현
    * 0보다 커야함

<br>

#### meter

* 값이 차지하는 크기 표시
* `<meter value="값" [속성="속성값"]></meter>`
* `<progress>` VS `<meter>`
  * 결과화면은 비슷
  * `<progress>` : 작업 진행 상황을 나타냄
  * `<meter>` : 전체 크기 중에서 얼마나 차지하는지를 표현

* 속성
  * `min`, `max` 
    * 범위의 최소, 최대값 지정
    * default : 0과 1
  * `value`
    * 범위 내에서 차지하는 값
  * `low`, `high`
    * "이 정도면 낮다/높다" 라고 할 정도의 값을 지정
  * `optimum`
    * "이 정도면 적당하다" 라고 할 정도의 범위 지정
    * optimum 값이 high 값보다 크다면 value 값이 클수록 좋고
    * optimum 값이 low 값보다 작다면 값이 작을수록 좋음

* 예시

  ```html
  <ul>
      <li>
      	<label> 점유율 : 0.8 </label>
          <!-- 전체크기 1을 기주으로 0.8만큼을 차지함을 의미 -->
          <meter value="o.8"></meter>
      </li>
  	<li>
      	<label> 트래픽 : 초과 </label>
          <!-- 전체크기는 1024~10240 인데, 높다고 설정한 8192보다 현재 값 9216이 더 크다는 것을 의미 -->
          <meter min="1024" max="10240" low="2048" high=8192 value="9216"></meter>
      </li>
      <li>
      	<label> 트래픽 : 적절 </label>
          <!-- 전체 1 중에서 현재 0.5를 차지하고 있으며 적정도를 0.8로 설정함을 의미 -->
          <meter value="0.5" optimum="0.8"></meter>
      </li>
  </ul>
  ```

<br>

---

<br>

## 공간 분할 태그

<br>

#### div & span

* div

  * **block 형식**으로 공간을 분할
  * 웹사이트의 레이아웃(전체 틀)을 만들 때 사용
  *  `div` 태그를 사용하여 각각의 블록(공간)을 알맞게 배치하고 CSS를 활용하여 스타일 적용

* span

  * **inline 형식**으로 공간을 분할
  * `<div>`와 `<p>`태그와 함께 웹페이지의 일부분에 스타일을 적용하기 위해 사용

* 차이점

  * `div`
    * 자동 줄 바꿈이 일어나면서 세로로 나열
    * 동일한 문장을 감쌌을 때
      * **박스 형태로 영역이 설정됨**
      * **그 안에 정렬됨**
    * margin : 4방향 모두 적용됨

  * `span`
    * 줄 바꿈이 일어나지 않고 가로로 나열
    * 동일한 문장을 감쌌을 때
      * **줄 단위로 영역이 설정됨**
      * **박스 형태가 아닌 텍스트가 노출되는 영역만 포함**
      * margin : 양옆으로만 적용됨

<br>

#### block & inline 형식 태그

* block 형식 태그

  * `div` 태그
  * `h1` ~ `h6` 태그
  * `p` 태그

  * `목록` 태그
  * `table` 태그
  * `form` 태그

* inline 형식 태그

  * `span` 태그

  * `a` 태그
  * `input` 태그

  * `글자 형식` 태그

