# Start Camp (3)

<br>

---

<br>

## Javascript

* 주로 웹 브라우저에서 사용하는 객체 기반의 스크립트 언어
* 인터프리터 언어

<br>

#### 별도의 파일 생성 후 html에 적용하기

1. `XXX.js` 파일 생성

2. 코드 작성

3. html 파일의 `<head>` 부분에 링크 코드 작성

   ```html
   <script src="./js/XXX.js"></script>
   ```

<br>

#### 변수 선언

1. `var`

   ```javascript
   var name = '김혜림'
   var name = '오혜림'
   ```

   * 단점
     * 변수를 한 번 더 선언했음에도 불구하고, 에러가 나오지 않음..
   * 코드량이 많아진다면 아주 치명적인 단점..
   * 그래서 ES6 이후, 이를 보완하기 위해 추가 된 변수 선언 방식이 `let`과 `const`

2. `let`

   ```javascript
   let name = '김혜림'
   let name = '오혜림' // error
   ```

   * `name`이 이미 선언 되었다는 에러 메시지가 나옴.

3. `const`

   ```javascript
   const name = '김혜림'
   const name = '오혜림' // error
   ```

   * `name`이 이미 선언 되었다는 에러 메시지가 나옴.

**Q. 그렇다면 `let`과 `const`의 차이점은?**

* `immutable` 여부!

* `let`은 변수에 재할당 가능

  ```javascript
  let name = '김혜림'
  name = '오혜림' // 재할당 가능
  ```

* `const`는 변수에 재할당 불가

  ```javascript
  const name = '김혜림'
  name = '오혜림' // error
  ```

<br>

#### 람다 표현식

```javascript
const test_func = () => console.log("~~~~~~~~~ test_func");
const min = (a,b) => a > b ? b : a;
```

<br>

#### 시간을 정해줘서 호출

* 일정 시간마다 호출

  ```javascript
  setInterval(test_func, 3000);
  ```
  * 3초마다 `test_func()`을 호출

* n초 후에 딱 한번 호출

  ```javascript
  setTimeout(test_func, 7000);
  ```

  * 7초 후에 `test_func()`을 호출

* n초 후에 일정 시간마다 호출했던 것을 멈춤

  ```javascript
  let func = setInterval(test_func, 3000); // 3초 시간마다 호출하는 함수
  setTimeout(function(){
  	clearInterval(func)
  }, 7000);
  ```

  * 일정 시간마다 호출하던 func을 n초 후에 정지시킴

<br>

---

<br>

## Spring project

#### import가 잘 안됐을 때

[maven] - [update project]

#### WordCloud 프로젝트

* Java Resource - src/main/resources - application.properties : 환경설정 파일

#### 서버 작동

* 프로젝트 마우스 우클릭 - Run As - Spring Boot App

#### 시작 URL

* `http://localhost:9999/startcamp/`