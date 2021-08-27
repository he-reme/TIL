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
  * 텍스트 box, 체크 box, 라디오 버튼 등 사용자가 데이터를 입력할 수 있도록 함
* `<textarea>`
  * 여러 줄의 문자를 입력할 수 있도록 함
* `<button>`
  * 버튼을 표시
* `<select>`
  * select box(드롭다운, 콤보box)를 표시
* `<optgroup>`
  * select box의 각 항목들을 그룹화 함.