# 객체

## window

* `window.alert("메시지")` 
  
* 사용자에게 메시지를 보여주고 확인받는 용도
  
* `window.prompt()`
  
  * 사용자로부터 데이터를 입력받는 용도
  
* `window.confirm()`
  
  * `예` 또는 `아니오` 둘 중 하나를 입력받는 용도
  
* `window.setInterval(함수, time)`

  * `time`마다 함수를 실행시킴

    ```javascript
    var displayDate = function()
    {
    	var d = new Date();
    	document.write(d.toLocaleString()+"<br>");
    };
    var time = 5000; //5초
    window.setInterval(displayDate,time);
    ```

  * 

## document

> 자바스크립트 내장 객체

#### (1) `document.getElement~()`

* 객체 참조

* **`Tag` 참조**

  * 단수

    ```
    var doms = document.getElementByTagName("button");
    ```

  * 복수

    ```
    var doms = document.getElementsByTagName("button");
    ```

    * `<button>태그`를 가진 객체가 n개이면, 먼저 등장한 순서대로 (위에서부터)
    * `doms[0], doms[1], ... , doms[n-1]` 로 접근

* **`Id` 참조**

  * 단수

    ```javascript
    var doms = document.getElementById("target");
    ```

  * 복수

    ```javascript
    var doms = document.getElementsById("target");
    ```



#### (2) `document.write()`

* 괄호 안의 내용을 브라우저에 출력

* **개행 비포함**

* 예시1

  ```javascript
  var v1 = "hello";
  document.write(v1 +"<br>");
  ```

  * `태그`를 넣어서 사용할 수 있음
    * `""` 를 사용

* 예시2

  ```javascript
  document.write("<ul>");
  var v1;
  document.write("<li>"+ v1 +"</li>"); // undefined
  document.write("<li>"+ typeof v1 +"</li>"); // undefined
  document.write("<li>"+ (v1+10) +"</li>"); // NaN (=Not a Number)
  v1 = 100;
  document.write("<li>"+ v1 +"</li>");
  document.write("<li>"+ typeof v1 +"</li>");
  document.write("<li>"+ (v1+10) +"</li>");
  v1 = true;
  document.write("<li>"+ v1 +"</li>");
  document.write("<li>"+ typeof v1 +"</li>");
  document.write("<li>"+ (v1+10) +"</li>");
  v1 = "가나다";
  document.write("<li>"+ v1 +"</li>");	
  document.write("<li>"+ typeof v1 +"</li>");
  document.write("<li>"+ (v1+10) +"</li>");
  document.write("<ul>");
  ```



#### (3) `document.writeln()`

* 괄호 안의 내용을 브라우저에 출력
* `document.write()` 와 다르게 **개행 포함**



---



## onclick

> 객체를 클릭했을 때 액션

* `변수.onclick`

  ```javascript
  var doms = document.getElementsByTagName("button");
  doms[0].onclick = function(){
  	window.alert("텍스트 버튼이 클릭되었어요!!"); 
  }
  doms[1].onclick = function(){
  	window.alert("이미지 버튼이 클릭되었어요!!")
  }
  ```



##