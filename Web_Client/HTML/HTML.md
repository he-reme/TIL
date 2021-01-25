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
		<meta "charset=UTF-8"> // 빼먹을 경우 한글 깨져서 나옴
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

  ````html
  <hr>
  ````

* 글씨 크기

  ```html
  <h1></h1>
  <h2></h2>
  ...
  <h6></h6>
  ```

* 하이퍼링크

  ```html
  <a href="URL"> 클릭 </a>
  ```

* 이미지 출력

  ````html
  <img src="URL" width="100" height="100">
  ````

  * `width`와 `height`는 생략 가능

* 이미지에 이름 붙이기

  ````html
  <figure>
  	<figcaption> 이름 </figcaption>
  	<img src="URL" width="100" height="100">
  </figure>
  ````

  * `<figcaption>`태그가 `<img>`태그 위에 있으면 위에, 아래에 있으면 아래에 이름이 붙음.

* 순서 있는 리스트

  ```html
  <ol>    
  	<li> 고기 </li>
  	<li> 치킨 </li>
  </ol>
  ```

* 순서 없는 리스트

  ```html
  <ul>    
  	<li> 고기 </li>
  	<li> 치킨 </li>
  </ul>
  ```

* 테이블

  ````html
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

  ```html
  <video width="720" height="400" controls>
  	<source src="동영상.mp4">
      <source src="동영상.ogg">
  </video>
  ```

  * 브라우저에 따라 확장자로 mp4를 인식할 수도, ogg를 인식할 수도 있으므로
    두개를 적어 놓으면 자동으로 인식하여 동영상을 보여줌. (참고: 크롬은 둘 다)

* `<>` 사용하기

  ```html
  &lt;jQuery도 조금 학습해요&gt;
  ```

  * HTML에서는 `<>`를 태그로 인식하려고 하기 때문에 없는 태그일 경우

    무시하고 화면에 렌더링 해주지 않음

    따라서 사용하고 싶은 경우, 특수문자 엔터티인 `&lt; &gt;`를 사용한다!

* 개행

  ```html
  <br>
  ```

* 단락 지정

  ```html
  <p>
  	1단락 입니다.
  </p>
  <!-- 여기서 개행 2번 됨 -->
  <p>
  	2단락 입니다.
  </p>
  ```

* 폼(form) - **텍스트 박스**

  * 기본

  ```html
  <form>
  	아이디 <input type="text" name="id" required>
  	패스퉈드 <input type="password" name="pwd" required>
  	<input type="submit" value="로그인"> <!-- 버튼 -->
  	<input type="reset" value="재작성">
  </form>
  ```

  * get 방식 - 입력값이 URL에 보임 (로그인에 사용하기에 적합하지 않음)

  ```html
  <form method="get" action="http://localhost:8000/edu/serverprogram">
          계정 <input type="text" name="account" required>
          패스워드 <input type="password" name="pwd" required>
          <input type="submit" value="로그인">
          <input type="reset" value="재작성">
  </form>
  ```

* 폼(form) - **check 박스**

  ```html
  <form method="get" action="http://localhost:8000/edu/serverprogram">
  	좋아하는 음식 (여러 개 선택) : <br>
      <input type="checkbox" name="food" value="f1">불고기<br>
      <input type="checkbox" name="food" value="f2">치킨<br>
      <input type="checkbox" name="food" value="f3" checked>피자<br>
      <input type="checkbox" name="food" value="f4">짜장면<br><br>
      <input type="submit" value="전송">
      <input type="reset" value="재작성">
  </form>
  ```

  * 여러 개 선택

* 폼(form) - **radio 박스**

  ```html
  <form method="get" action="http://localhost:8000/edu/serverprogram">
  	좋아하는 칼라 (한 개 선택) : <br>
      <input type="radio" name="color" value="노란색">노란색<br>
      <input type="radio" name="color" value="녹색">녹색<br>
      <input type="radio" name="color" value="주황색">주황색<br><br>
      <input type="submit" value="전송">
      <input type="reset" value="재작성">
  </form>
  ```

  * 한 개 선택

* 폼(form) - **드롭다운**

  * 업엔 다운 - `min/max`로 지정

  ```html
  <form method="get" action="http://localhost:8000/edu/serverprogram">
  	태어난 년도를 입력하세요 : <br>
      <input type="number" name="age" min="2000" max="2005"><br><br>
      <input type="submit" value="전송">
      <input type="reset" value="재작성">
  </form>
  ```

  * 리스트 다운 - 직접 지정

  ```html
  <form method="get" action="http://localhost:8000/edu/serverprogram">
  	태어난 년도를 선택하세요 : <br>
      <select name="year">
      	<option value="2000">2000</option>
          <option value="2001">2000</option>
          <option value="2002">2002</option>
          <option value="2003">2003</option>
          <option value="2004">2004</option>
      </select><br><br>
      <input type="submit" value="전송">
      <input type="reset" value="재작성">
  </form>
  ```

* 폼(form) - **긴 텍스트 상자**

  ```html
  <form method="get" action="http://localhost:8000/edu/serverprogram">
  	남기려는 글을 입력하세요 : <br>
      <textarea name="memo" rows="5" cols="50"></textarea><br>
      <input type="submit" value="전송">
      <input type="reset" value="재작성">
  </form>
  ```

* 폼(form) - **달력**

  ```html
  <form method="get" action="http://localhost:8000/edu/serverprogram">
  	생일을 선택하세요 : <br>
      <input type="datetime-local" name="birth"><br><br> <!-- 년월일시간 -->
      <input type="date" name="birth"><br><br> <-- 년월일 -->
      <input type="submit" value="전송">
      <input type="reset" value="재작성">
  </form>
  ```

  

