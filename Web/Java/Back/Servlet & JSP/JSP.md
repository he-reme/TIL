# JSP

> Java Server Page

* HTML 내에 자바 코드를 삽입하여 웹 서버에서 동적으로 웹 페이지를 생성하여 웹 브라우저에 돌려주는 언어
* 웹 애플리케이션 서버에서 동작
* **JSP는 실행시에는 자바 서블릿으로 변환된 후 실행되므로**
  * 서블릿과 거의 유사
  * 하지만, 서블릿과는 달리 HTML 표준에 따라 작성되므로 웹 디자인하기에 편리함

<br>

---

<br>

## 스크립팅 요소

#### 1. 선언

```jsp
<%! 멤버변수와 method 작성 %>
```

* 멤버변수 선언이나 메소드를 선언하는 영역

<br>

#### 2. 스크립트릿 (Scriptlet)

```jsp
<% java code %>
```

* 서비스 메서드
  * Client 요청 시 매번 호출되는 영역
  * Servlet으로 변환 시 service() method에 해당되는 영역

* request, response에 관련된 코드 구현

<br>

#### 3. 표현식

```jsp
<%= 변수명 or 문자열 %>
```

* 브라우저에 출력할 때 사용

* `<% out.print(변수명 or 문자열); %>` 와 같은 표현

* 주의
  * 변수명 or 문자열 뒤에 세미콜론(`;`) 작성 X

<br>

#### 4. 주석

```jsp
<%-- 주석 --%>
```

* HTML 주석과 다른점
  * `<!-- 클라이언트에게 보임 -->`
  * `<%-- 서버로 넘겨지기 때문에 클라이언트에게 보이지 않음 --%>`

<br>

---

<br>

## 지시자

> Directive

#### 1. page Directive

```jsp
<%@ page attr1="val1" attr2="val2" ... %>
```

* 컨테이너에게 현재 JSP 페이지를 어떻게 처리할 것인가에 대한 정보를 제공

* 속성

  * language
    * 스크립트에서 사용 할 언어 지정
    * 기본값 : `java`

  * info
    * 현재 JSP 페이지에 대한 설명
  * contentType
    * 브라우저로 내보내는 내용의 MIME 형식 지정 및 문자 집합 지정
    * 기본값 : `text/html; charset=ISO-8859-1`
  * pageEncoding
    * 현재 JSP 페이지 문자 집합 지정
    * 기본값 : `charset=ISO-8859-1`
  * import
    * 현재 JSP 페이지에서 사용할 java 패키지나 클래스 지정
    * 예: `import = "java.util.*, java.io.*"`
  * session
    * 세션의 사용 유무 설정
    * 기본값 : `true`

<br>

#### 2. include Directive

```jsp
<%@ include file="/template/header.jsp" %>
```

* 특정 jsp file을 페이지에 포함
* 여러 jsp페이지에서 반복적으로 사용되는 부분을 jsp file로 만든 후 반복 영역에 include 시켜 반복되는 코드를 줄일 수 있음

<br>

#### 3. taglib Directive

```jsp
%@ taglib prefix="c" url="http://hereme.com/jsp/jstl/core" %>
```

* JSTL 또는 사용자에 의해서 만든 커스텀 태그를 이용할 때 사용됨
* JSP 페이지 내에 불필요한 자바 코드를 줄일 수 있음

* `긴 url`을 `문자 c`를 사용해서 쓸거다~

<br>

---

<br>

## 기본 객체

* request ★
  * Type : `javax.servlet.http.HttpServletRequest`
  * HTML 폼 요소의 선택 값 등 사용자 입력 정보를 읽어올 때 사용

* response ★
  * Type : `javax.servlet.http.HttpServletResponse`
  * 사용자 요청에 대한 응답을 처리하기 위해 사용

* pageContext
  * Type : `javax.servlet.jsp.PageContext`
  * 각종 기본 객체를 얻거나 forward 및 include 기능을 활용할 때 사용
* session ★
  * Type : `javax.servlet.http.HttpSession`
  * 클라이언트에 대한 세션 정보를 처리하기 위해 사용
  * page directive의 session 속성을 false로 하면 내장 객체는 생성이 안됨
* application
  * Type : `javax.servlet.ServletContext`
  * 웹 서버의 애플리케이션 처리와 관련된 레퍼런스하기 위해 사용
  * application = 프로젝트

* out ★
  * Type : `javax.servlet.jsp.JspWriter`
  * 사용자에게 전달하기 위한 output 스트림을 처리할 때 사용
* config
  * Type : `javax.servlet.ServletConfig`
  * 현재 JSP에 대한 초기화 환경을 처리하기 위해 사용
* page
  * Type : `java.lang.Object`
  * 현재 JSP 페이지에 대한 참조 변수에 해당됨
  * like 자바의 `this`
* exception
  * Type : `java.lang.Exception`
  * Error를 처리하는 JSP에서 isErrorPage속성을 true로 설정하면 exception 내장 객체를 사용할 수 있음
  * 전달된 오류 정보를 다 담고 있는 내장 객체
  * 기본값 : false

<br>

#### 기본 객체의 영역 (Scope)

* 범위
  * pageContext < request < session < application

* **pageContext**

  * 하나의 JSP 페이지를 처리할 때 사용되는 영역
  * 한 번의 클라이언트 요청에 대하여 하나의 JSP 페이지가 호출되며
  * 이때 단 한 개의 page 객체만 대응 됨
  * 페이지 영역에 저장한 값은 페이지를 벗어나면 사라짐

  * 커스텀 태그에서 새로운 변수를 추가할 때 사용
  * 사용 범위
    * 생성한 JSP 내에서만 사용

* **request **★★★

  * 하나의 HTTP 요청을 처리할 때 사용되는 영역
  * 웹 브라우저가 요청을 할 때마다 새로운 request 객체 생성됨
  * request 영역에 저장한 속성은 그 요청에 대한 응답이 완료되면 사라짐
  * 사용 범위
    * 요청을 한 JSP와 요청을 받은 JSP 페이지에서만 사용

* **session **★★★

  * 하나의 웹 브라우저와 관련된 영역
  * 같은 웹브라우저 내에서 요청되는 페이지들은 같은 session들을 공유하게 됨
  * 로그인 정보 등을 저장함
  * 사용 범위
    * 같은 프로젝트 내 모든 JSP 사용
    * 대신 `session = true` 로 설정한 페이지에서만 사용~
      * 인증된 페이지만 사용 가능하다는 말~!!

* **application**

  * 하나의 웹 어플리케이션과 관련된 영역
  * 웹 어플리케이션당 1개의 application 객체가 생성됨
  * 같은 웹 어플리케이션에서 요청되는 페이지들은 같은 application 객체를 공유함
  * 사용 범위
    * 같은 프로젝트 내 모든 JSP 사용
    * 제약조건 없이! 인증 필요 없이! 사용 가능

<br>

#### 기본 객체의 영역 (Scope) - 공통 method

* servlet과 jsp 페이지 간에 특정 정보를 주고 받거나 공유하기 위한 메소드를 지원
* `void setAttribute (String name, Object value)`
  * 문자열 name 이름으로 Object형 데이터를 저장함
  * Object형이므로 어떠한 java 객체도 저장 가능
* `Object getAttribute(String name)`
  * 문자열 name에 해당하는 속성 값이 있다면 Object 형태로 가져오고 없으면 null 리턴
  * 따라서 리턴 값에 대한 적절한 형 변환이 필요함
* `Enumeration getAttributeNames()`
  * 현재 객체에 저장된 속성들의 이름들을 Enumeration 형태로 가져옴
* `void removeAttribute(String name)`
  * 문자열 name에 해당하는 속성을 삭제함

<br>

---

<br>

## Web Page 이동

* request를 가지고 다음 페이지로 이동하기

  ```
  request.setAttribute(-);
  ```

<br>

#### 방법1 : `forward(request, response)`

* 사용 방법

  ```jsp
  RequestDispatcher dispatcher = request.getRequestDispatcher(path);
  dispatcher.forward(request, response);
  ```

* 이동 범위
  * **동일 서버 (project) 내 경로**
    * `https://naver.com/`를 지정할 수 없다는 말
  * path
    * context_root 생략하고 써야함!!!! 
    * 기본이 context_root 아래 경로에 접근 하기 때문~
* location bar
  * 기존 URL 유지
  * 실제 이동되는 주소 확인 불가
* 객체
  * **기존의 request와 response가 그대로 전달**
* 속도
  * 비교적 빠름
* 데이터 유지
  * request의 `setAttribute(name, value)`를 통해 전달

<br>

#### 방법2 : `sendRedirect(location)`

* 사용 방법

  ```jsp
  response.sendRedirect(location);
  ```

* 이동 범위
  * 동일 서버 포함 타 URL 가능
* location bar
  * 이동하는 page로 변경
* 객체
  * **기존의 rquest와 response는 소멸**되고
  * 새로운 request와 response가 생성
* 속도
  * `forward()` 에 비해 느림
* 데이터 유지
  * **request로는 data 저장 불가능**
    * 기존 것들은 소멸되기 때문
  * **session이나 cookie를 이용**

