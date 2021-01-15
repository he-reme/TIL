# CSS

> Casecading(계층적인) Style Sheets

* HTML 태그에 의해서 웹 페이지가 출력(렌더링)될 때  스타일을 조정할 수 있는 기술

* 구조적으로 짜여진 문서(`HTML, XML`)에 `Style`을 적용하기 위해 사용하는 것

* 예시1 - **인라인 방법**

  * `h1` 태그마다 스타일이 다른 경우

  ```html
  <h1 style = "color:orange; background-color:green">올라프</h1>
  ```

* 예시2  - **전역적 방법**

  * 모든 `h1` 태그에 `color`은 `orange`, `background-color`은 `green`를 적용시키고 싶은 경우
* `<head>` 태그에 작성
  
  ```html
  <style> 
  	h1{
  		color:orange; 
  		background-color:green
  	}
  </style>
```
  

* 예시3 - **외부 파일 연결 방법**

  * 독립된 파일(확장자.css)을 만들어서 HTML 문서에 연결하는 방법
    * 사용하려는 `HTML`파일의 `<head>` 태그에 작성 

  ```
  <link rel="stylesheet" type="text/css" href="style.css"/>
  ```

  

---



## 사용 시 주의사항

* 단위를 꼭 붙여야 한다.
  * 예시
    * px
    * pt
    * em
    * %

* 속성들은.. `css3-cheat-sheet.pdf` 참고!



---



## CSS 선택자

> 일단 주로 사용할 것 같은 것만 정리해봄.. 추후 공부하면서 추가 예정

### (1) id 선택자

* `#id {color : green;}`

```html
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        #t1 {
            color : green;
        }
        #t2 {
            color : red;
        }
    </style>
</head>
<body>
	<h2 id="t1">둘리</h2>
	<h2 id="t2">도우너</h2>
</body>
</html>
```



### (2) 가상 선택자

* 예시) `:hover`

  * 사용자가 대상 요소 위에 마우스를 올렸을 때 스타일 적용

  ```html
  <!DOCTYPE html>
  <html lang="ko">
  <head>
      <meta charset="UTF-8">
      <title>Title</title>
      <style>
          a {
              text-decoration : none;
          }
          a:hover {
              font-weight : bold;
          }
          img:hover {
              opacity : 0.3; /* 투명도 0.0~1.0 (완전불투명) */
          }
  
      </style>
  </head>
  <body>
  	<a href="http://www.naver.com/">네이버</a>
  	<hr>
  	<img src="/edu/images/totoro.png">
  </body>
  </html>
  ```



### (3) 클래스 선택자

* `.클래스이름 {color:red;}`

  ```html
  <!DOCTYPE html>
  <html lang="ko">
  <head>
      <meta charset="UTF-8">
      <title>Title</title>
      <style>
          div {
              margin-left:auto;
              margin-right:auto;
          }
          div.test {
              background-color : lime;
          }
      </style>
  </head>
  <body>
  	<div class="test"> 
          <h1> 안녕 </h1> 
      </div>
  </body>
  </html>
  ```

  

---



## 공간 태그

> HTML 태그지만 CSS를 사용하지 않으면 잘 사용 안함.

### (1) `<div></div>`

* 블럭 스타일
* 블럭으로 공간을 잡음 
  * width, height 지정 가능

```html
<style>
	div{
		background-color : lime;
		margin : 5px;
		width : 300px
		height : 200px
		font-size : 1.5em
		padding : 10px;
	}
```

* 위의 div 크기 : 320*220
  * width, height는 content크기이고,
  * padding이 위아래, 좌우에 있기 때문에

### (2) `<span></span>`

* 인라인 스타일
* 딱 맞게 공간을 잡음 
  * width, height 지정 불가
  * 예외는 `<img>` 태그



---

