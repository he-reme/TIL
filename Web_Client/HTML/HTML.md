# HTML

> Hyper Text Markup Language

* 텍스트, 이미지,동영상 등을 어떻게 표현할지를 정하는 언어로서 마크업 방식으로 구현
* [HTML 태그 공부 - w3schools.com](https://www.w3schools.com/)

* 공부 환경

  * 웹 서버 소프트웨어 : `nginx`
  * HTML 작성 툴 : `pycharm`

  

---



## 5가지 기본 요소

> HTML5 문서의 작성



### (1) 태그(tag)

* 의미

  * `<`와 `>`로 둘러싸인 문자열
  * 시작태그`<>`와 종료태그`</>`로 구성
  * 문서 표현 방식을 지시

* 예시

  `<title>웹문서내용</title>`

  * `<title></title>`



### (2) 내용(content)

* 의미

  * 태그로 둘러싸인 문자열

* 예시

  `<title>웹문서내용</title>`

  * `웹문서내용`

  

### (3) 엘리먼트(element)

* 의미

  * 태그와 내용을 포함한 전체 문자열
  * HTML 문서의 기본 구성 단위
  * (상위) 엘리먼트 안에 (하위) 엘리먼트가 계층적으로 포함될 수 있음

* 예시

  `<title>웹문서내용</title>`

  * `<title>웹문서내용</title>`

<title>`웹문서내용`< 

### (4) 속성(attribute)

* 의미

  * 엘리먼트의 상세한 표현(기능) 설정 사항을 지시
  * 시작 태그 안에 사용

* 예시

  `<title color="red"></title>`

  * `color`



### (5) 속성값(value)

* 의미
  * 속성값 `' '` 또는 `" "`로 감싸야 함
* 예시
  * `<title color="red"></title>`
    * `red`



---



## HTML5 문서 구조

```html
<!-- HTML 문서 -->

<!-- 선언문 -->
<!DOCTYPE HTML>

<!-- HTML요소 -->
<html>
	<!-- HEAD 요소 -->
	<head>
		<meta "charset=UTF-8">
		<title> HTML5 기본 구조 </title>
	</head>

	<!-- BODY요소 -->
	<body>
		<!-- 문서의 내용 -->
		<p align="center"> HTML5에 대하여 학습 </p>
	</body>
</html>
```



---



## 예시 코드

### nginx

##### (1) 기본 세팅

* 포트번호 : `8000`
* 웹 서버 시작 : `nginx.exe` 
* 웹 서버 끝 : `nginxstop.bat`
* 정상적으로 작동하는 지 확인 : `http://localhost/8000/`

##### (2) nginx를 이용한 생성한 `html 파일` 실행시키기

* 경로

  * [`nginx-1.18.0` 폴더] - [`html` 폴더]

* **nginx는 위의 경로의 `html 파일`을 실행시킴**

  * 경로 안에 새로운 폴더도 생성 가능

* 실행 방법

  * `C:\KHR\nginx-1.18.0\html\edu` 경로인 경우

    * `http://localhost:8000/edu/first.html`

    

### 태그

* 가로선

  ````python
  <hr>
  ````

* 글씨 크기

  ```python
  <h1></h1>
  <h2></h2>
  ...
  <h6></h6>
  ```

* 하이퍼링크

  ```python
  <a href="URL"> 클릭 </a>
  ```

* 이미지 출력

  ````python
  <img src="URL" width="100" height="100">
  ````

  * `width`와 `height`는 생략 가능

* 이미지에 이름 붙이기

  ````python
  <figure>
  	<figcaption> 이름 </figcaption>
  	<img src="URL" width="100" height="100">
  </figure>
  ````

  * `<figcaption>`태그가 `<img>`태그 위에 있으면 위에, 아래에 있으면 아래에 이름이 붙음.

* 순서 있는 리스트

  ```python
  <ol>    
  	<li> 고기 </li>
  	<li> 치킨 </li>
  </ol>
  ```

* 순서 없는 리스트

  ```python
  <ul>    
  	<li> 고기 </li>
  	<li> 치킨 </li>
  </ul>
  ```

* 테이블

  ````python
  <table border="">
  	<tr><th>번호</th><th>이름</th></tr>
      <tr><td>1번</td><td>김혜림</td></tr>
      <tr><td>2번</td><td>이세모</td></tr>
      <tr><td>3번</td><td>박네모</td></tr>
  </table>
  ````
  * `border` 속성 : 선 긋기
  * `tr`: 행단위  `th`: 제목행  `td`: 일반행

* 동영상 출력

  ```python
  <video width="720" height="400" controls>
  	<source src="동영상.mp4">
      <source src="동영상.ogg">
  </video>
  ```

  * 브라우저에 따라 확장자로 mp4를 인식할 수도, ogg를 인식할 수도 있으므로
    두개를 적어 놓으면 자동으로 인식하여 동영상을 보여줌. (참고: 크롬은 둘 다)