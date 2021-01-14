# CSS

> Casecading(계층적인) Style Sheets

* HTML 태그에 의해서 웹 페이지가 출력(렌더링)될 때  스타일을 조정할 수 있는 기술

* 예시1 - **인라인 방법**

  * `h1` 태그마다 스타일이 다른 경우

  ```html
  <h1 style = "color:orange; background-color:green">올라프</h1>
  ```

* 예시2  - **전역적인 방법**

  * 모든 `h1` 태그에 `color`은 `orange`, `background-color`은 `green`를 적용시키고 싶은 경우

  ```html
  <style>
  	h1{
  		color:orange; 
  		background-color:green
  	}
  </style>
  ```

  