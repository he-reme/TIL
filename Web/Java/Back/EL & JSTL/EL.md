# EL

> Expression Language
>
> 화면에 뿌린다

#### EL?

* 표현을 위한 언어
* JSP 스크립트의 표현식을 대신하여 속성 값을 쉽게 출력하도록 고안된 language
* 즉 표현식 `<%= %>`을 대체할 수 있음
* EL 포현식에서 도트 연산자 왼쪽은 
  * 반드시 `java.util.Map` 객체 또는 `java Bean` 객체여야 함
* EL 표현시에서 도트 연산자 오른쪽은 
  * 반드시 맵의 키이거나 Bean 프로퍼티여야 함

<br>

#### EL에서 제공하는 기능

* JSP의 네가지 기본 객체가 제공하는 영역의 속성 사용
* 자바 클래스 메소드 호출 기능
* 표현 언어만의 기본 객체 제공
* 수치, 관리, 논리 연산 제공

<br>

---

<br>

## EL 문법

#### 스크립트릿을 EL로

* 스크립트릿

  ```javascript
  <%= ((com.ssafy.model.MemberDto) request.getAttribute("userinfo")).getZipDto().getAddress() %>
  ```

* EL

  ```
  ${userinfo.zipDto.address}
  ```

  * `address` 프로퍼티 
    * `getAddress()` 에서 추출한 이름
      1. get, set 생략
      2. 제일 앞 대문자는 소문자로

<br>

#### Map을 사용하는 경우

```
${ Map.Map의 키 }
```

<br>

#### Java Bean을 사용하는 경우

```
${ Java Bean.Bean 프로퍼티}
```

<br>

---

<br>

#### `[]` 연산자

* EL에는 Dot 표기법 외에 `[]` 연산자를 사용하여 객체의 값에 접근할 수 있음
* `[]` 연산자 안의 값이 문자열인 경우, 이것은 맵의 키가 될 수도 있고, Bean 프로퍼티나 리스트 및 배열의 인덱스가 될 수 있음
* 배열과 리스트인 경우, 문자로 된 인덱스 값은 숫자로 변경하여 처리함
* 이외엔 일반적으로 Dot 표기법 더 많이 사용

* `[]` 연산자를 이용한 객체 프로퍼티 접근

  ```java
  ${userinfo["name"]}
  ```

* Dot 표기법을 이용한 객체 프로퍼티 접근

  ```java
  %{userinfo.name}
  ```

* 리스트나 배열 요소에 접근

  ```java
  // Servlet
  String[] names = {"홍길동", "이순신", "임꺽정"};
  request.setAttribute("userNames", names);
  
  // JSP
  ${userNames[0]}
  ${userNames["1"]}
  ```

<br>

---

<br>

## EL 내장 객체

> JSP 페이지의 EL 표현식에서 사용할 수 있는 객체

#### JSP

* `pageContext`
  * 타입
    * Java Beans
  * 설명
    * 현재 페이지의 프로세싱과 상응하는 PageContext instance

<br>

#### 범위 (scope)

* `pageScope`
  * 타입
    * Map
  * 설명
    * page scope에 저장된 객체를 추출
* `requestScope` ★
  * 타입
    * Map
  * 설명
    * request scope에 저장된 객체를 추출
* `sessionScope` ★
  * 타입
    * Map
  * 설명
    * session scope에 저장된 객체를 추출
* `applicationScope`
  * 타입
    * Map
  * 설명
    * applicatino scope에 저장된 객체를 추출

<br>

#### 요청 매개변수

* `param` ★
  * 타입
    * Map
  * 설명
    * `ServletRequest.getParameter(String)`을 통해 요청 정보를 추출
* `paramValues`
  * 타입
    * Map
  * 설명
    * `ServletRequest.getParameterValues(String)`을 통해 요청 정보를 추출

<br>

#### 요청 헤더

* `header`
  * 타입
    * Map
  * 설명
    * `HttpServletRequest.getHeader(String)`을 통해 헤더 정보를 추출
* `headerValues`
  * 타입
    * Map
  * 설명
    * `HttpServletRequest.getHeaders(String)`을 통해 헤더 정보를 추출

<br>

#### 쿠키

* `cookie` ★
  * 타입
    * Map
  * 설명
    * `HttpServletRequest.getCookies()`을 통해 쿠키 정보를 추출

<br>

#### 초기화 매개변수

* `initParam`
  * 타입
    * Map
  * 설명
    * `ServletContext.getInitParameter(String)`을 통해 초기화  파라미터를 추출

<br>

---

<br>

## EL 사용

* pageContext를 제외한 모든 EL 내장 객체는 **Map**
  * key와 value 쌍으로 값을 저장하고 있음

<br>

#### 기본 문법

```
${expr}
```

<br>

#### EL에서 객체 접근 ★

* `request.setAttribute("userinfo", "김혜림");`

  1. `${requestScope.userinfo}`
  2. `${pageContext.request.userinfo}`
  3. `${userinfo}`
     * 프로퍼티 이름만 사용할 경우 자동으로
     * pageScope > requestScope > sessionScope > applicationScope 순으로 객체를 찾음

* `url?name=김혜림&fruit=사과&fruit=바나나`

  1. `${param.name}`
  2. `${paramValues.fruit[0]}.${paramValues.fruit[1]}`

* EL에서 request 객체 접근

  ```jsp
  Method is : ${pageContext.request.method}
  
  // Servlet
  request.setAttribute("ssafy.user", memberDto);
  
  // Case #1 : 에러
  ${ssafy.user.name} // ssafy라는 속성은 존재하지 않음
  
  // Case #2 : request 내장 객체에서 [] 연산자를 통해 속성 접근
  ${requestScope["ssafy.user"].name}
  ```

  * `.`이 있는 속성이면 `[]` 를 통해 접근할 수 있음

* `${cookie.id.value}`

  1. Cookie가 null이라면 null return
  2. null이 아니라면 id를 검사 후 null이라면 null return
  3. null이 아니라면 value값 검사
     * EL은 값이 null이라도 null을 출력하지 않는다
     * 공백 출력

  * 스크립트릿을 통한 쿠키 값 출력

    ```java
    Cookie[] cookies = request.getCookies();
    for(Cookie cookie : cookies) {
    	if(cookie.getName().equals("userId")) {
    		out.println(cookie.getValue());
    	}
    }
    ```

  * EL 내장 객체를 통한 쿠키 값 출력

    ```
    ${cookie.userId.value}
    ```

<br>

#### EL 연산자

* 대부분 java와 동일
* 산술
  * `+`, `-`, `*`, `/`, `%`
* 관계형
  * `==` 혹은 `eq`
  * `!=` 혹은 `ne`
  * `<` 혹은 `lt`
  * `>` 혹은 `gt`
  * `<=` 혹은 `le`
  * `>=` 혹은 `ge`
* 3항 연산
  * `조건? 값1 : 값2`
* 논리
  * `&&` 혹은 `and`
  * `||` 혹은 `or`
  * `!` 혹은 `not`
* 타당성 검사 ★
  * `empty`
  * 사용
    * `${empty var}`
  * empty 연산자에서 true를 return하는 경우
    1. 값이 null일 때
    2. 값이 빈 문자열(`""`)일 때
    3. 길이가 0인 배열일 때
    4. 빈 Map 객체일 때
    5. 빈 Collection 객체일 때

<br>

#### EL에서 객체 method 호출

```
<%
List<MemberDto> list = dao.getMembers();
request.setAttribute("users", list);
%>
```

* 회원 수

  ```
  ${requestScope.users.size()}
  ${users.size()}
  ```

* 주의

  ```
  ${users.size <%= request.getAttribute("users").getSize() %>
  ```

  