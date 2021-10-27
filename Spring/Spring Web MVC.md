# Spring Web MVC

#### MVC Pattern

* 어플리케이션의 확장을 위해 Model, View, Controller 세가지 영역으로 분리
* 컨포넌트의 변경이 다른 영역 컴포넌트에 영향을 미치지 않음 (유지보수 용이)
* 컴포넌트 간의 결합성이 낮아 프로그램 수정이 용이 (확장성이 뛰어남)

<br>

#### 특징

* Spring은 DI나 AOP같은 기능 뿐만 아니라, Servlet 기반의 Web 개발을 위한 MVC Framework를 제공
* Spring MVC는 Model2 Architecture와 Front Controller Pattern을 Framework 차원에서 제공
* Spring MVC Framework는 Spring을 기반으로 하고 있기 때문에 Spring이 제공하는 Transaction 처리나 DI 및 AOP 등을 손쉽게 사용

<br>

---

<br>

## MVC Pattern

> Model - View - Controller

#### Model

* 어플리케이션 상태의 캡슐화
* 상태 쿼리에 대한 응답
* 어플리케이션의 기능 표현
* 변경을 view에 통지

<br>

#### View

* 모델을 화면에 시각적으로 표현
* 모델에게 업데이트 요청
* 사용자의 입력을 컨트롤러에 전달
* 컨트롤러가 view를 선택하도록 허용

<br>

#### Controller

* 어플리케이션의 행위 정의
* 사용자 액션을 모델 업데이트와 mapping
* 응답에 대한 view 선택

<br>

---

<br>

## Spring MVC 구성요소

> setting을 통해 Spring이 자동 구현해주는 것들..

#### DispatcherServlet

* Front Controller
* 모든 클라언트의 요청을 전달 받음
* Controller에게 클라이언트의 요청을 전달하고, Controller가 리턴 한 결과값을 View에게 전달하여 알맞은 응답을 생성

<br>

#### HandlerMapping

* 클라이언트의 요청 URL을 어떤 Controller가 처리할지를 결정
* URL과 요청 정보를 기준으로 어떤 핸들러 객체를 사용할지 결정하는 객체이며, DispatcherServlet은 하나 이상의 핸들러 매핑을 가질 수 있음

<br>

#### Controller

* 클라이언트의 요청을 처리한 뒤, Model을 호출하고 그 결과를 DispatcherServlet에 알림

<br>

#### ModelAndView

* Controller가 처리한 데이터 및 화면에 대한 정보를 보유한 객체

<br>

#### ViewResolver

* Controller가 리턴 한 뷰 이름을 기반으로 Controller의 처리 결과를 보여줄 View를 결정

<br>

#### View

* Controller의 처리 결과를 보여줄 응답 화면을 생성

<br>

---

<br>

## Spring MVC 실행 순서

1. DispatcherServlet이 요청을 수신
   * 단일 Front Controller Servlet
   * 요청을 수신하여 처리를 다른 컨포넌트에 위임
   * 어느 Controller에 요청을 전송할지 결정
2. DispatcherServlet은 Handler Mapping에 어느 Controller를 사용할 것인지 문의
   * URL과 Mapping
3. DispatcherServlet은 요청을 Controller에게 전송하고 Controller는 요청을 처리한 후 결과 리턴
   * Business Logic 수행 후 결과 정보(Model)가 생성되어 JSP와 같은 View에서 사용됨
4. ModelAndView Obeject에 수행결과가 포함되어 DispatcherServlet에 리턴
5. ModelAndView는 실제 JSP정보를 갖고 있지 않으며, ViewResolver가 논리적 이름을 실제 JSP 이름으로 변환
6. View는 결과 정보를 사용하여 화면을 표현함

<br>

---

<br>

## Spring MVC 구현

#### Spring MVC를 이용한 Application 구현 Step

* web.xml에 DispatcherServlet 등록 및 Spring 설정파일 등록
* 설정 파일에 HandlerMapping 설정
* Controller 구현 및 Context 설정 파일(servlet-context.xml)에 등록
* Controller와 JSP의 연결을 위해 View Resolver 설정
* JSP 코드 작성

<br>

#### Controller 작성

* 좋은 디자인은 Controller가 많은 일을 하지 않고 Service에 처리를 위임

<br>

#### 설정 파일

* `servlet-context.xml` 
  * web 관련된 설정
  * DispatcherServlet의 할일 정의!!! 

* `root-context.xml` 
  * web에 비관련 설정
  * 데이터 소스 설정 (DB 연동)

<br>

#### web.xml ★★★

* DispatcherServlet 설정

* `<init-param>`을 설정하지 않으면 `<servlet-name>-servlet.xml` file에서 applicationContext 의 정보를 load

* Spring Contatiner는 설정파일의 내용을 읽고 ApplicationContext 객체를 생성

* `<url-pattern>`은 DispatcherServlet이 처리하는 URL Mapping pattern을 정의

* Servlet이므로 1개 이상의 DispatcherServlet 설정 가능

* `<load-on-startup>1</load-on-startup>` 설정 시 Was startup시 초기화 작업 진행

* web.xml : DispatcherServlet 설정 부분

  ```xml
  <servlet>
  	<servlet-name>appServlet1</servlet-name>
  	<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
  	<init-param>
  		<param-name>contextConfigLocation</param-name>
  		<param-value>/WEB-INF/spring/appServlet/servlet-context.xml1</param-value>
  	</init-param>
  	<load-on-startup>1</load-on-startup>
  </servlet>
  		
  <servlet-mapping>
  	<servlet-name>appServlet1</servlet-name>
  	<url-pattern>*.do</url-pattern>
  </servlet-mapping>
  
  <!-- 여러개의 DispatcherServlet 추가 가능 -->
  
  <servlet>
  	<servlet-name>appServlet2</servlet-name>
  	<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
  	<init-param>
  		<param-name>contextConfigLocation</param-name>
  		<param-value>/WEB-INF/spring/appServlet/servlet-context.xml2</param-value>
  	</init-param>
  	<load-on-startup>1</load-on-startup>
  </servlet>
  		
  <servlet-mapping>
  	<servlet-name>appServlet2</servlet-name>
  	<url-pattern>*.action</url-pattern>
  </servlet-mapping>
  ```
  * DispatcherServlet을 여러 개 설정 가능
  * 각 DispatcherServlet마다 각각의 Application Context 생성

* 최상위 Root ContextLoader 설정

  * Context 설정 파일들을 로드하기 위해 web.xml 파일에 리스너 설정

    * ContextLoaderListener

    ```xml
    <!-- Creates the Spring Container shared by all Servlets and Filters -->
    <listener>
    	<listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>
    ```

  * 리스너가 설정되면 `/WEB_INF/spring/root-context.xml` 파일을 읽어서 공통적으로 사용되는 최상위 Context를 생성

  * 그 외의 다른 컨텍스트 파일들을 최상위 어플리케이션 컨텍스트에 로드하기 위해서는

    ```xml
    <!-- The definition of the Root Spring Container shared by all Servlets and Filters -->
    <context-param>
    	<param-name>contextConfigLocation</param-name>
    	<param-value>/WEB-INF/spring/root-context.xml</param-value>
    </context-param>
    ```

<br>

#### Controller Class

* Controller Class 작성

  ```java
  @Controller
  public class HomeController {
  	private static final Logger logger = LoggerFactory.getLogger(HomeController.class);
  	
  	@RequestMapping(value="/", method=RequestMethod.GET)
  	public String home(Locale locale, Model model) {
  		logger.info("Welcome home! the client locale is {}.", locale);
  		model.addAttribute("message", "안녕하세요!!");
  		return "index";
  	}
  }
  ```

* Context 설정 파일이에 Controller 등록

  * `servlet-context.xml`

  ```xml
  <beans:bean class="com.test.web.HomeController"/>
  ```

* Controller와 response page 연결을 위한 ViewResolver 설정

  * `servlet-context.xml`

  ```xml
  <!-- Resolves views selected for rendering by @Controllers to .jsp resources in the /WEB-INF/views directory -->
  <beans:bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
  	<beans:property name="prefix" value="/WEB-INF/views/" />
  	<beans:property name="suffix" value=".jsp" />
  </beans:bean>
  ```

  * 이를 통해 jsp 이름만 보내도 jsp 파일로 만들어줌

<br>

---

<br>

## @Controller

> Controller Class는 Client의 요청을 처리

#### `@Controller`와 `@RequestMapping` 선언

* `@RequestMapping("/user")`
* 클래스와 메소드에 mapping 가능
* DefaultAnnotationHandlerMapping과 AnnotationHandlerAdapter를 사용
  * Spring 3.0부터는 기본 설정이므로 별도의 추가 없이 사용 가능

<br>

#### `@Controller` 선언

* Class 타입에 적용
* Spring 3.0부터는 `@Controller` 사용 권장

<br>

#### Controller Class 자동 스캔

* `context:component-scan` 선언
* base-package에 설정된 package내의 class 중 `@Controller `annotation이 적용된 클래스는 자동 스캔 대상이 됨

```xml
<context:component-scan base-package="com.test.user.controller"/>
```

<br>

#### Controller method의 HTTP method에 한정

* 같은 URL 요청에 대하여 HTTP method(GET, POST)에 따라 서로 다른 메소드를 mapping할 수 있음

```java
@RequestMapping(value="/index.do" method=RequestMethod.GET)

@RequestMapping(value="/index.do" method=RequestMethod.POST)
```

```
@GetMapping("/index.do")
@PostMapping("/index.do")
```

<br>

#### Controller에 `@RequestMapping`을 설정하지 않으면?

* HTTP ERROR 404

<br>

#### `@RequestParam` 을 이용한 parameter mapping

```
URL 호출
http://localhost/web/index.do?name=김혜림&age=25
```

```
@RequestMapping(value="/index.do", method=RequestMethod.GET)
public String test(@RequestParam("name") String name, @RequestParam("age") int age, Model model) {
	...
}
```

* 다른 사용법도 있음!

  * 필수 여부 설정

    ```java
    @RequestParam(value="name", required=false)
    ```
    * true이면 값이 반드시 넘어와야 함. 안넘어오면 error 발생

  * 기본값 설정

    ```java
    @RequestParam(value="age", defaultValue="25")
    ```

<br>

#### HTML form과 Command Object

* Command Object
  * DTO, Vo
* SpringMVC는 form에 입력한 data를 JavaBean 객체를 이용해서 전송할 수 있음

* List로 받는 것도 가능

<br>

#### View에서 Command 객체에 접근

* Command 객체는 자동으로 반환되는 Model에 추가됨

* Controller의 `@RequestMapping` method에 전달받은 Command 객체에 접근

  ```
  @RequestMapping(value="/write.do", method=RequestMethod.GET)
  public String write(BoardDto boardDto) {
  	return board/writer;
  }
  ```

  ```
  ${boardDto.title}
  ${boardDto.content}
  ```

  * request에 저장되는 Command 객체의 이름
    * BoardDto 의 첫글자를 소문자로 변경한 것

* @ModelAttribute를 사용하여 View에서 사용할 Command 객체의 이름 변경 가능

  ```
  @RequestMapping(value="/write.do", method=RequestMethod.GET)
  public String write(@ModelAttribute("article") BoardDto boardDto) {
  	return board/writer;
  }
  ```

  ```
  ${article.title}
  ${article.content}
  ```

<br>

#### `@CookieValue`를 이용한 Cookie mapping

* author라는 이름으로 authorValue 변수값을 입력하여 쿠키를 만듦

```java
public String hello(@CookieValue("author") String autorValue) {
	return "ok";
}
```

```java
public String hello(@CookieValue(value="author", required=false, defaultValue="user") String autorValue) {
	return "ok";
}
```

<br>

#### `@RequestBody` parameter type

* HTTP 요청 Body가 그대로 객체에 전달됨
* AnnotationMethodHandler Adapter에는 HttpMessageConverter 타입의 메시지 변환기가 기본으로 여러 개 등록되어 있음
* `@RequestBody`가 붙은 parameter가 있으면 해당 미디어 타입을 확인 후 처리 가능한 변환기(Converter)가 자동으로 객체를 변환시켜 줌
* 주로 `@ResponseBody`와 함께 사용됨

<br>

#### Servlet API 사용

* HttpSession의 생성을 직접 제어해야 하는 경우
* Controller가 Cookie를 생성해야 하는 경우
* Servlet API를 선호하는 경우

<br>

#### Controller Class에서 method의 return type 종류

* ModelAndView
  * model 정보 및 view 정보를 담고있는 ModelAndView 객체
* Model
  * view에 전달할 객체 정보를 담고있는 Model을 반환
  * 이때 view 이름은 요청 URL로부터 결정됨
  * RequestToViewNameTranslator
* String
  * view에 전달할 객체 정보를 담고있는 map을 반환
  * 이때 view 이름은 요청 URL로부터 결정됨
  * RequestToViewNameTranslator
* String
  * view의 이름을 반환
* View
  * view 객체를 직접 리턴
  * 해당 View 객체를 이용해서 view를 생성
* void
  * method가 ServletResponse나 HttpServletResponse 타입의 parameter를 갖는 경우 method가 직접 응답을 처리한다고 가정
  * 그렇지 않을 경우 요청 URL로부터 결정된 View를 보여준다
  * RequestToViewNameTranslator
* @ResponseBody Annotation 적용
  * method에서 @ResponseBody annotation이 적용된 경우, 리턴 객체를 HTTP응답으로 전송
  * HttpMessageConverter를 이용해서 객체를 HTTP 응답 스트림으로 변환함

<br>

---

<br>

## View

> 이어서 더 정리해야함.... ㅎ

* Controller에서는 처리 결과를 보여줄 View 이름이나 객체를 리턴하고, DispatcherServlet은 View 이름이나 View 객체를 이용하여 view를 생성
  * 명시적 지정
  * 자동 지정

<br>

#### ViewResolver

* 논리적 view와 실제 JSP 파일 mapping

* servlet-context.tml

  ```xml
  <beans:bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
  	<beans:property name="prefix" value="/WEB-INF/views/" />
  	<beans:property name="suffix" value=".jsp" />
  </beans:bean>
  ```

  * InternalResourceViewResolver

    * `prefix + 논리뷰 + suffix` 로 설정

    * 예) board/list가 요청되면
      * `/WEB-INF/views/board/list.jsp` 로 설정됨

* View 이름 명시적 지정

  * ModelAndView 혹은 String 타입으로 리턴

  * 방법1 : ModelAndView 생성과 동시에 초기화

    ```java
    @Controller
    public class HomeController {
    	@RequestMapping("/write.do")
    	public ModelAndView write() {
    		ModelAndView mav = new ModelAndView("write");
    		return mav;
    	}
    }
    ```

  * 방법2 : ModelAndView 생성 후 값 대입

    ```java
    @Controller
    public class HomeController {
    	@RequestMapping("/write.do")
    	public ModelAndView write() {
    		ModelAndView mav = new ModelAndView();
    		mav.setViewName("write");
    		return mav;
    	}
    }
    ```

  * 방법3 : String 타입으로 반환

    ```java
    @Controller
    public class HomeController {
    	@RequestMapping("/write.do")
    	public String write() {
    		return "write";
    	}
    }
    ```

    

