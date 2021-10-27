# Back-End 공부

#### 환경

* eclipse
* mysql
* apache tomcat
* dynamic web project

<br>

#### 공부 순서

1. Servlet (XXX.java)
2. JSP (XXX.jsp)
3. Cookie & HttpSession
4. EL & JSTL
5. MVC

<br>

---

<br>

#### Servlet과 JSP

* JSP는 실행시에는 자바 Servlet으로 변환된 후 실행됨

* JSP 혹은 Servlet 안에는 Java, HTML 코드 모두 쓸 수 있음

  * 그러나 이는 가독성도 안좋고, 프로젝트 유지보수도 어려움

  * JSP

    * 기본적으로 HTML 태그를 사용하고 
    * `<% %>` 안에 Java 코드 작성

  * Servlet

    * 기본적으로 Java 코드를 작성하고 

    * `PrintWriter`를 통해 HTML 태그 사용

      ```java
      PrintWriter out = response.getWriter();
      out.println("<HTML태그> 안뇽 <HTML태그>");
      ```

      

* 따라서!!!

  * JSP에는 HTML
    * Client에게 보여주는 화면만 구성
  * Servlet은 java
    * Data get, Logic call만
  * 하도록 하면 좋아용

<br>

---

<br>

#### EL 과 JSTL

* EL 과 JSTL를 사용하면
* JSP에 `<% %>` 표현식을 없애줘서 JSP에는 HTML 태그만
* Servlet에는 Java 코드만
* 작성하도록 하여 가독성을 높여준다.

<br>

---

<br>

#### MVC

* JSP를 사용한 웹 개발에 MVC 패턴 적용하면!!
* JSP (HTML)
  * **View**
  * Client에게 보여주는 화면만 구성
  * Servlet에 요청
  * Client에 응답
* Servlet (Java)
  * **Controller**
  * 클라이언트 요청 분석 후 Data get
  * Logic call
  * data를 가지고 Service 호출
  * 결과에 따른 응답 페이지로 이동

* Service
  * **Model**
  * Business Logic
  * data를 가지고 DAO 호출
  * 예) 페이징 처리
* DAO
  * **Model**
  * DataBase Logic

* 데이터 전달 시 담는 그릇
  * **Model**
  * DTO, VO를 같은 개념으로 보는 곳도 많지만.. 프로젝트에 따라 분리해서 사용하기도 함
  * DTO
    * Data Transfer Object
    * data를 전달할 때 쓰는 데이터 구조
      * 주로 Data Table 구조 구현할 때
  * VO
    * Value Object
    * 단순한 데이터
    * Data Table 보다는 내가 조합해서 쓰고 싶을 때 

