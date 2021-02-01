# jQuery

> HTML 문서 안의 스크립트 코드를 단순화하도록 설계된 **자바스크립트 라이브러리**

* 라이브러리 선언
* 자식
* 주요 메소드
* 메소드
* CSS 메소드
* 이벤트

* 그림 그리기 소스코드 (예시)

---



## jQuery 라이브러리 선언

* jQuery 라이브러리를 포함하는 `<script>` 태그를 작성

  ```html
  <script src="http://code.jquery.com/jquery-xxx.js"></script>
  ```

* jQuery에서 제공되는 메서드 호출하는 방식 (2가지)
  1. `jQuery(자바스크립트객체).xxx()`
  2. `jQuery.xxx()`
* `jQuery()`함수의 표시 : **`$()`**
  * 코드 안의 `jQuery()` 함수는 식별이 어렵고 불편하기 때문에 줄여서 표시
  * `$(dom객체).xxx()`
    * `$(dom객체, dom객체, ...).xxx()` : 여러 객체 지정
    * `$('*')` : 모든 객체 선택
  * `$('CSS선택자').xxx()`
    * `$('CSS선택자, CSS선택자, ...').xxx()` : 여러 선택자 지정
  * `$(함수)` 
    * `load` 이벤트 발생시 자동으로 호출
    * `$(document).ready()`
  * `$.xxx()` : jQuery 객체가 제공하는 클래스 메소드 (객체 생성하지 않고 바로 사용할 수 있는 함수)



---



## 자식

#### (1) 모든 자식태그 가져오기

```javascript
$('부모태그 *').xxx();
```

* 주로 `<ul>`태그에 사용

#### (2) 특정 자식태그 가져오기

```javascript
$('부모태그 > 부모의자식태그 > 부모의자식태그의자식태그').xxx();
```



---



## 주요 메소드

> **$(객체).xxx()**
>
> 값 가져오기 : getter
>
> 값 추가하기 : setter

#### html

> = innerHTML
>
> 첫번째 객체만 (여러 개일 때)

* 값 가져오기

  * `html()`

* 값 추가하기

  * `html("문자열") `
  * `html(함수)`

* 모든 객체에 적용하기

  ```javascript
  $(document).ready(function(){
  	$(객체).html(function(index, html)
  	{
  		return index + " " + html;
  	});
  });
  ```

  * 첫번째 인자는 무조건 `index`가 아규먼트로 주어짐

#### text

> = textContent
>
> 모든 객체 (여러 개일 때)

* 값 가져오기
  * `text()`
* 값 추가하기
  * `text("문자열") `
  * `text(함수)`

#### val

> = value
>
> 첫번째 객체만 (여러 개일 때)

* 값 가져오기
  * `val()`
* 값 추가하기
  * `val("문자열")`
  * `val(함수)`

#### css

> CSS 속성
>
> 첫 번째 객체만

* 값 가져오기
  * `css("CSS속성명")`
* 값 추가하기
  * `css("CSS속성명", "CSS속성값")`
  * `css("CSS속성명". 함수)`
  * `css(자바스크립트객체)`

#### attr

> HTML 태그 속성

* 값 가져오기
  * `attr("HTML태그속성명")`
* 값 추가하기
  * `attr("HTML태그속성명", "HTML태그속성값")`
  * `attr("HTML태그속성명". 함수)`
  * `attr(자바스크립트객체)`
* 속성 삭제하기
  * `removeAttr("HTML태그속성")`

#### class

> 태그의 클래스

* 클래스 추가하기
  * `addClass('추가할클래스명')`
* 클래스 삭제하기
  * `removeClass('삭제할클래스명')`



#### ★ 여러 객체 처리 도와주는 코드

> 첫번째 객체만 처리하는 메소드를 위한 

* **`each` 메소드 사용**

```javascript
$(document).ready(function(){
	$(객체).each(function(index, data){
		var color = $(data).css('color');
		alert(color);
	});
});
```

* **배열 사용**

  ```javascript
  <h1>Header-0</h1>
  <h1>Header-1</h1>
  <h1>Header-2</h1>
  <script>
      $(document).ready(function () {
          var color = ['Red', 'White', 'Purple'];
          $('h1').css('color', function (index) {
              return color[index];
          });
      });
  </script>
  ```

* **`function(index)` 사용**

  ```javascript
  $(document).ready(function(){
  	$(객체).html(function(index, html)
  	{
  		return index + " " + html;
  	});
  });
  ```

  * 첫번째 인자는 무조건 `index`가 아규먼트로 주어짐



---



## 메소드

#### first

* 첫번째 객체 지정

```javascript
$('태그명').first();
```

#### remove

* 해당 객체 모두 삭제

```javascript
$('태그명').remove();
```

* 첫번째만 삭제하고 싶을 때

```javascript
$('태그명').first().remove();
```

#### empty

* 해당 태그의 자식들 모두 삭제

```javascript
$('태그명').empty(); // 해당 태그는 살아있음!!
```

#### appendTo

* 태그에 해당 객체를 추가

```javascript
$(객체).appendTo('태그명');	
```

* 예시

  ```javascript
   $(document).ready(function () {
              $('<h1></h1>').html('Hello World .. !').appendTo('body');
              $('<h1>안녕하세요.... !</h1>').appendTo('body');
  ```

  * `<body>` 태그에 해당 객체를 추가

#### append

* 태그에 해당 객체를 추가

```javascript
$('태그명').append(객체1, 객체2, 객체3, ...);	
```



---



## CSS

> 메소드

```javascript
$(dom객체).css('속성', '값');
```

* 예시: `$('h1').css('color', 'red')`



#### (1) id

```javascript
$('#id').css('속성', '값');
$('태그#id').css('속성', '값'); // $('h1#target').css('color', 'red')
```



#### (2) 클래스

````javascript
$('.클래스명').css('속성', '값');
$('태그.클래스명').css('속성', '값');
````

* 클래스 여러개일 때

  ```javascript
  $('.클래스명1.클래스명2').css('속성', '값'); // 두 클래스 모두 가지고 있는 객체 찾기
  $('.클래스명1:not(클래스명2)').css('속성', '값'); // 클래스1은 가지고 클래스2는 가지지 않는 객체 찾기
  ```

  * 예시

    ```javascript
    <head>
        <meta charset="utf-8">
        <script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
        <script>
            $(document).ready(function () {
                $('.item.select').css('border', '2px solid black');
                $('.item:not(.select)').css('border', '2px solid green');
            });
        </script>
    </head>
    <body>
        <h1 class="item">.item:not(.select)에 불려짐</h1>
        <h1 class="item select">.item.select에 불려짐</h1> 
        <h1 class="select">불려지지 않음</h1>
    </body>
    ```

    * 태그 안에 클래스를 여러 개 지정하고 싶을 때
    * **공백**을 통해 여러개 지정할 수 있음



---



## 이벤트

### 이벤트 핸들러 구현

> 여러 개 이벤트 연결 가능

#### (1) `$(객체).on('이벤트명',함수)`

* 예시

  ```javascript
  $(document).ready(function () {
  	$('h1').on('click', function () {
      	// 이벤트 발생 시 실행할 코드
      });
  });
  ```

#### (2) `$(객체).on(자바스크립트객체)`

* 예시

  ```javascript
  $(document).ready(function () {
  	$('h1').on({
      	mouseenter: function () { $(this).addClass('reverse'); },
          mouseleave: function () { $(this).removeClass('reverse'); }
      });     
  });
  ```

#### (3) `$(객체).이벤트명(함수)`

* 예시

  ```javascript
  $(document).ready(function () {
  	// hover는 함수 2개 사용해야 함 (add, remove)
  	$('h1').hover(function () {
      	$(this).addClass('reverse');
      }, function () {
      	$(this).removeClass('reverse');
      });
      $('#two').click(function () {
      	$(this).html(function (index, html) {
          	 return '★' + html;
          });
      });
  });
  ```

  

#### (4) `$(객체).one('이벤트명', 함수)`

* 한 번만 수행

* 예시

  ```javascript
  $(document).ready(function () {
      $('h1').one('click', function () {
      // 이벤트 발생 시 실행할 코드
      });
  });
  ```

* `one` 이용하지 않는 이벤트 한 번만 수행하기

  ```javascript
  $(document).ready(function () {
      $('h1').on('click', function () {
      	// 이벤트 발생 시 실행할 코드
      	$(this).off(); // 이벤트 연결 제거
  	});
  });
  ```

  * `$(this).off()` : 이벤트 연결 제거



### 기본 이벤트 제거

```javascript
객체.preventDefault();
```



---



## 그림 그리기 소스코드 (예시)

```html
<!DOCTYPE html>
<html>
<head>
<script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
<script>
	var toggle =true;
	$(document).ready(function() {
		// 변수를 선언합니다.
		var canvas = document.getElementById('draw');
		var context = canvas.getContext('2d');

		// 이벤트를 연결합니다.
		$(canvas).click(function(event) {
			// 위치를 얻어냅니다.
			if (toggle) {				
				var position = $(this).offset();
				var x = event.pageX - position.left;
				var y = event.pageY - position.top;
				// 선을 그립니다.
				context.beginPath();
				context.moveTo(x, y);
				toggle = false;
			} else {				
				var position = $(this).offset();
				var x = event.pageX - position.left;
				var y = event.pageY - position.top;
				// 선을 그립니다.
				context.lineTo(x, y);
				context.strokeStyle = 'red';
				context.stroke();
				toggle = true;
			} 
		});
	});
</script>
</head>
<body>
	<canvas id="draw" width="500" height="300"
		style="border: 1px solid black;">

    </canvas>
</body>
</html>
```



---



## 글자수 텍스트 폼 소스코드 (예시)

> 150 자 시작, 초과 시 음수로 표현 

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <script src="http://code.jquery.com/jquery-3.5.1.min.js"></script>
    <script>
        $(document).ready(function (event) {
            $('textarea').keydown(function () {
                // 남은 글자 수를 구하기
                var inputLength = $(this).val().length;
                var remain = 150 - inputLength;

                // 남은 글자 수 출력
                $('h1').html(remain);

                // 150자 초과 시 숫자 색상 변경
                if (remain >= 0) {
                    $('h1').css('color', 'Black');
                } else {
                    $('h1').css('color', 'Red');
                }
            }); 
        });
</script>
</head>
<body>
    <div>
        <p>입력하세요</p>
        <h1>150</h1>
        <textarea cols="70" rows="5"></textarea>
    </div>
</body>
</html>
```

