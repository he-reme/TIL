# Servlet

<br>

#### 자바 서블릿

* 자바를 사용하여 웹페이지를 동적으로 생성하는 서버측 프로그램 혹은 그 사양을 말함

* 흔히 서블릿이라고 불림
* 웹 서버의 성능을 향상하기 위해 사용하는 자바 클래스의 일종

<br>

#### JSP와 Servlet 비교

* JSP
  * HTML 문서 안에 Java코드를 포함
* Servlet 
  * 자바 코드 안에 HTML을 포함

<br>

#### Life Cycle

* Servlet class는 main method가 없음
  * 즉, 객체의 생성부터 사용의 주체가 사용자가 아닌 Servlet Container에게 있음
* Client가 요청을 하게 되면 Servlet Container는 Servlet 객체를 생성(한번만)하고, 초기화(한번만)하며 요청에 대한 처리(요청시마다 반복)를 하게 됨
* 또한 Servlet객체가 필요 없게 되면 제거하는 일까지 Container가 담당함

* 주요 method
  * `init()`
    * 서블릿이 코드에 로드 될 때 한번 호출
    * 코드 수정으로 인해 다시 로드되면 다시 호출
  * `doGet()`
    * GET 방식으로 data 전송 시 호출
  * `doPost()`
    * POST 방식으로 data 전송 시 호출
  * `service()`
    * 모든 요청은 `service()`를 통해서 `doXXX()` 메소드로 이동
  * `destroy()`
    * 서블릿이 메모리에서 해제되면 호출
    * 코드가 수정되면 호출

<br>

---

<br>

## Web Architecture

#### Client

* Web Browser
  * data 발생
  * 요청 request

<br>

#### Server

* Web Server
  * Client 접속, 응답 처리
  * 웹을 통해서 클라이언트가 서버에 접속하게 도와줌
    * 데이터 전송만 가능
  * 응답 response
    * MarkUp Language로 응답
      * html, xml, json, txt, ...

* Application Server
  * Client 요청에 대한 Logic 처리
  * Presentation
    * 일처리를 하고 난 후의 결과
    * 결과를 MarkUp Language로 만듦
      * html, xml, json, txt, ...
  * Business Logic
    * 일처리 (Service)
  * Persistence Logic
    * 일처리 (Service)
    * Persistence : 데이터베이스
    * Web Server와 DBMS를 연결
      * JDBC 사용
* RDBMS
  * DataBase
* Web Application Server
  * WAS
  * Web Server + Application Server
  * web에서 java (서블릿)이 돌아가도록 함

<br>

---

<br>

## Project

> Dynamic Web Project

<br>

#### Context root

* `/` 입력 시 : `https://hereme.com/` 으로 접속 가능
* `h` 입력 시 : `https://hereme.com/h/`로 접속 가능

<br>

#### 프로젝트 폴더 구조

* 프로젝트 폴더
  * src
    * java 파일
  * WebContent
    * java를 제외한 모든 파일
    * html, css, js, img, jsp

<br>

#### Servlet

* Interface
  * `implements Servlet`
  * `destroy()`, `init()`, `service()` 모두 직접 구현..
    * 대신 `service()`만 필수
* 추상 클래스
  * `extends GenericServlet`
    * `destroy()`. `init()` 등은 이미 구현됨
    * `service()` 만 추상 메서드
      * 필수로 직접 구현해야 함
  * **`extends HttpServlet`**
    * 추상 메서드 없음
    * `Override`를 통해 구현 
    * 보통 이를 상속받아서 구현함!!

<br>

#### Servlet 파일 생성

* URL mappings
  * 해당 Servlet 접근 주소
  * 설정 방법
    * 방법1 : 이클립스에서 servlet 파일 생성 시 설정 가능
    * 방법2 : 파일 내에서 `@WebServlet("/XXX")`를 수정하여 설정 가능
  * 예
    * 해당 Servlet의 URL mappings가 `XXX` 라면?
    * `https://hereme.com/h/XXX/` 로 접근 가능

* Page 이동
  * Get 방식
    * URL 입력
    * link 클릭
    * form - get
  * Post 방식
    * form - post