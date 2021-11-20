# JSP

#### Web Application Architecture

* JSP를 이용하여 구성할 수 있는 Web Application Archetecture
  * 크게 model1과 model2로 나뉨
  * model1
    * JSP가 client의 요청에 대한 Logic 처리와 response page(view)에 대한 처리를 모두 함
  * model2
    * JSP가 response pace(view)에 대한 처리만 함
* model2 구조는 MVC Pattern을 web 개발에 도입한 구조

<br>

---

<br>

## Model1 구조

* view와 logic을 JSP 페이지 하나에 처리하는 구조
* client로부터 요청이 들어오게 되면 JSP 페이지는 
  * java beans나 별도의 service class를 이용하여 작업을 처리, 
  * 결과를 client에 출력함
* 간단한 page를 구성하기 위해 과거에 가장 많이 사용되었던 architecture

<br>

#### Model1 구조의 장단점

* 장점
  * 구조가 단순하여 직관적
  * 개발시간 적어, 개발 비용 적음

* 단점
  * 출력을 위한 view(html) 코드와 로직 처리를 위한 java 코드가 섞여 있기 때문에 JSP 코드 자체가 복잡해 짐
  * JSP 코드에 Back-End와 Front-End가 혼재되기 때문에 분업이 힘들어짐
  * project의 규모가 커지게 되면 코드가 복잡해 지므로 유지보수 하기가 어려워 짐
  * 확장성(신기술의 도입, framework 등...)이 나쁨

<br>

---

<br>

## Model2 구조

* 모든 처리를 JSP 페이지에서 하는 것이 아니라

* client 요청에 대한 처리
  * servlet 담당
* logic처리
  * java class (Service, Dao, ...) 담당
* client에게 출력하는 response page
  * jsp 담당

* MVC pattern을 웹개발에 도입한 구조이며 완전히 같은 형태를 보임

<br>

#### MVC

* **Model**
  * Service, DAO, Java Beans
  * Logic(Business & DB) 을 처리하는 모든 것
  * Controller로부터 넘어온 data를 이용하여 이를 수행하고 그에 대한 결과를 다시 Controller에 return
* **View**
  * JSP
  * 모든 화면 처리를 담당
  * Client의 요청에 대한 결과 뿐 아니라 Controller에 요청을 보내는 화면단도 jsp에서 처리
  * Logic 처리를 위한 Java code는 사라지고 결과 출력을 위한 code만 존재
* **Controller**
  * Servlet
  * Client의 요청을 분석하여 Logic처리를 위한 Model단을 호출
  * return 받은 결과 data를 필요에 따라 request, session 등에 저장하고,
  * redirect 또는 forward 방식으로 jsp(View) page를 이용하여 출력함

<br>

#### Model2 구조의 장단점

* Model1의 단점을 보완하기 위해 만들어 졌으나, 다루기 어렵다
* 장점
  * 출력을 위한 view(html) 코드와 로직 처리를 위한 java 코드가 분리 되었기 때문에 JSP는 Model1에 비해 코드가 복잡하지 않음
  * 화면단과 Logic단이 분리 되었기 때문에 분업이 용이
  * 기능에 따라 code가 분리 되었기 때문에 유지보수 쉬움
  * 확장성 뛰어남
* 단점
  * 구조가 복잡하여 초기 진입이 어려움
  * 개발 시간의 증가로 개발 비용 증가

<br>

---

<br>

## Model2 구조 한 눈에 보기

>  Model2 : JSP를 사용한 웹 개발에 MVC 패턴 적용

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

<br>

