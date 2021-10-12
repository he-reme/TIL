# JSTL

> JSP Standard Tag Library

* XML 데이터 처리와 조건문, 반복문, 국제화, 지역화 같은 일을 처리하기 위한 JSP 태그 라이브러리

<br>

---

<br>

## JSTL Tag

#### directive 선언 형식

```
<%@ taglib prefix="prefix" uri="uri" %>
```

<br>

#### library

* core ★
  * prefix
    * c
  * function
    * 변수 지원, 흐름제어,  URL 처리
  * URI
    * `http://java.sun.com/jsp/jstl/core`
* XML
  * prefix
    * x
  * function
    * XML 코어, 흐름제어, XML 변환
  * URI
    * `http://java.sun.com/jsp/jstl/xml`
* 등등

<br>

---

<br>

## JSTL Core Tag

* 선언

  ```
  <%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
  ```

* 변수 지원
  * `set` ★
    * jsp page에서 사용할 변수 설정
  * `remove`
    * 설정한 변수를 제거
* 흐름제어
  * `if `★
    * 조건에 따른 코드 실행
  * `choose`, `when`, `otherwise` ★
    * 다중 조건을 처리할 때 사용
    * `if~else if ~ else`
  * `forEach` ★
    * array나 collection의 각 항목을 처리할 때 사용
* URL 처리
  * `forTokens`
    * 구분자로 분리된 각각의 토큰을 처리할 때 사용
    * `StringTokenizer`
  * `import`
    * URL을 사용하여 다른 자원의 결과를 삽입
  * `redirect`
    * 지정한 경로로 redirect
  * `url`
    * URL 작성
* 기타 태그
  * `catch`
    * Exception 처리에 사용
  * `out`
    * JspWriter에 내용을 처리한 후 출력

<br>

---

<br>

## JSTL Core Tag 사용

#### `<c:set>`

* 변수 선언
* 변수나 특정 객체의 프로퍼티에 값을 할당할 때 사용
* 새로운 변수 선언
  * `<c:set var="변수명" value="값"></c:set>`
* 특정 객체의 프로퍼티에 값 할당
  * `<c:set target="특정객체" value="값" property="프로퍼티"></c:set>`
* scope 속성
  * 변수의 생존 범위
  * 디폴트는 page
  * page | request | session | application

<br>

#### `<c:catch>`

* 예외
* 기본적으로 JSP 페이지는 예외가 발생하면 지정된 오류페이지를 통해 처리함
* `<c:catch>` 액션은 JSP 페이지에서 예외가 발생할 만한 코드를 오류페이지로 넘기지 않고 직접 처리할 때 사용

<br>

#### `<c:if>`

* 조건문

* test 속성

  * 조건문 작성
  * 해당 속성에 지정된 표현식을 평가하여 결과가 true인 경우 액션의 Body 컨텐츠를 수행

* var 속성

  * 표현식의 평과 결과인 boolean 값을 담을 변수를 나타냄
  * scope 속성
    * 변수의 생존 범위 설정

* 예시

  ```jsp
  <c:if test="${empty userinfo}">
  ...
  </c:if>
  ```

<br>

#### `<c:choose>`, `<c:when>`, `<c:otherwise>`

* 조건문

* `<c:choose>`, `<c:when>`, `<c:otherwise>` 액션을 사용하면 if, else if, else와 같이 처리할 수 있음

* 예시

  ```jsp
  <c:choose>
  
  	<c:when test="${userType == 'admin'}">
  		관리자 화면...
  	</c:when>
  	
  	<c:when test="${userType == 'member'}">
  		회원 사용자 화면...
  	</c:when>
  	
  	<c:otherwise>
  		일반 사용자 화면
  	</c:when>
  	
  </c:choose>
  ```

<br>

#### `<c:forEach>`

* 반복문
* **컬렉션에 있는 항목들에 대하여 액션의 Body 컨텐츠를 반복하여 수행**
* 컬렉션로 올 수 있는 것들
  * Array, Coolection, Map, 콤마로 분리된 문자열

* var 속성
  * 반복에 대한 현재 항목을 담는 변수를 지정
* items 속성
  * 반복할 항목들을 갖는 컬렉션을 지정
* varStatus 속성
  * 이 속성에 지정한 변수를 통해 현재 반복의 상태를 알 수 있음

* 예시

  ```jsp
  <c:forEach var="article" items="${ articles }">
  
  <table class="table table-active text-left">
  	<tbody>
  		<tr class="table-info">
  			<td>작성자 : ${ article.userName } </td>
  			<td class="text-right"> 작성일 : ${ article.regTime } </td>
  		</tr>
  		<tr>
  			<td colspan="2" class="table-danger">
  				<strong> ${ article.articleNo }. ${ article.subject }</strong>
  			</td>
  		</tr>
  		<tr>
  			<td class="p-4" colspan="2"> ${ article.content } </td>
  		</tr>
  	</tbody>
  </table>
  
  </c:forEach>
  ```

  * articles(컬렉션)를 찾고, 해당 컬렉션에 있는 항목들을 article이라는 변수로 순차 접근 

<br>

---

<br>

#### 사용 예제

* JSTL 적용 전

  ```jsp
  <%
  String root = request.getContextPath();
  %>
  ```

* JSTL 적용 후

  ```jsp
  <%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
  
  <c:set var="root" value="${pageContext.request.contextPath}" />
  ```


<br>

---

<br>

