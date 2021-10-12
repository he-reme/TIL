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
  * Servlet은 java 코드를 짜서
  * forward나 sendRedirect를 사용하여 

<br>

---

<br>

#### EL 과 JSTL

* EL 과 JSTL를 사용하면
* JSP에 `<% %>` 표현식을 없애줘서 JSP에는 HTML 태그만
* Servlet에는 Java 코드만
* 작성하도록 하여 가독성을 높여준다.
