# 의존성 주입

> DI : Dependency Injection

<br>

---

<br>

## 빈 생성범위

#### 싱글톤 빈

* 스프링 빈은 기본적으로 싱글톤으로 만들어짐

  * 그러므로, 컨테이너가 제공하는 모든 빈의 인스턴스는 항상 동일함

* 컨테이너가 항상 새로운 인스턴스를 반환하게 만들고 싶을 경우

  * `scope`를 `prototype`으로 설정해야 함

* 예시

  * 방법1 : annotation

  ```java
  @Component("memberService")
  @Scope("singleton")
  public class MemberServiceImple implements MemberService{
  	...
  }
  ```

  * 방법2 : xml configuration file

  ```xml
  <bean id="" class="" scope="prototype"></bean>
  ```

< br>

#### 빈의 생성 범위 지정

* singleton

  * 스프링 컨테이너당 하나의 인스턴스 빈만 생성
  * default

* prototype

  * 컨테이너에 빈을 요청할 때마다 새로운 인스턴스 생성

* request

  * HTTP Request별로 새로운 인스턴스 생성
  * web에서만 실행됨

* session

  * HTTP Session별로 새로운 인스턴스 생성

  * web에서만 실행됨

<br>

---

<br>

## 스프링 빈 설정

#### 스프링 빈 설정 메타 정보

* 메타 정보의 표현 방법
  * XML Document
  * Annotation
  * Java Code
* 사용
  * xml
  * xml + annotation
  * annotation + java code
    * 이 조합을 제일 많이 씀

<br>

#### 스프링 빈 설정 : XML

* XML문서 형태로 빈의 설정 메타 정보를 기술
* 단순하며 사용하기 쉬움. 직관적
* 가장 많이 사용하는 방식
* `<bean>` 태그를 통해 세밀한 제어 사용

<br>

#### 스프링 빈 설정 : Annotation

* 어플리케이션의 규모가 커지고 빈의 개수가 많아질 경우 XML 파일을 관리하는 것이 번거로움
* 빈으로 사용될 클래스에 특별한 annotation을 부여해 주면 자동으로 빈 등록 가능
* **오브젝트 빈 스캐너**로 **빈 스캐닝**을 통해 자동 등록
  * 빈 스캐너는 기본적으로 클래스 이름을 빈의 아이디로 사용
  * 정확히는 클래스 이름의 첫 글자만 소문자로 바꾼 것을 사용

* Annotation으로 빈을 설정할 경우 반드시 component-scan을 설정해야 함

  ```
  <beans ...>
  	<context:component-scan base-package="com.test.hello.*"/>
  </beans>
  ```

* Stereotype annotation 종류

  * 빈 자동등록에 사용할 수 있는 annotation

  * 빈 자동인식을 위한 annotation이 여러가지인 이유

    * 계층별로 빈의 특성이나 종류를 구분
    * AOP Pointcut 표현식을 사용하면 특정 annotation이 달린 클래스만 설정 가능
    * 특정 계층의 빈에 부가기능 부여

  * Stereotype

    * `@Repository`

      * DAO 또는 Repository 클래스에 사용

    * `@Service`

      * 서비스 계층의 클래스에 사용

    * `@Controller`

      * MVC 컨트롤러에 사용

    * `@Component`

      * 위 3개의 계층 구분을 적용하기 어려운 일반적인 경우에 설정

    * `@Configuration`

      * annotation + java code 조합쓸 때

      * applicationContext.xml 대신 java클래스를 사용했을 때

      * 설정 파일임을 나타내줌 

      * 예시

        * ApplicationConfig.java

        ```java
        package com.ssafy.configuration;
        
        import javax.sql.DataSource;
        
        import org.springframework.context.annotation.Bean;
        import org.springframework.context.annotation.ComponentScan;
        import org.springframework.context.annotation.Configuration;
        import org.springframework.jdbc.datasource.SimpleDriverDataSource;
        
        @Configuration
        @ComponentScan(basePackages = {"com.ssafy.model"})
        public class ApplicationConfig {
        	
        	@Bean
        	public DataSource getDataSource() {
        		SimpleDriverDataSource dataSource = new SimpleDriverDataSource();
        		dataSource.setUrl("jdbc:mysql://127.0.0.1:3306/dbname?serverTimezone=UTC&useUniCode=yes&characterEncoding=UTF-8");
        		dataSource.setDriverClass(com.mysql.cj.jdbc.Driver.class);
        		dataSource.setUsername("hereme");
        		dataSource.setPassword("1111");
        		return dataSource;
        	}
        }
        ```

        * Main.java

          ```java
          // ApplicationConfig.java 설정
          ApplicationContext context = new AnnotationConfigApplicationContext(ApplicationConfig.class);	
          ```

          

<br>

---

<br>

## Dependency Injection

* 객체 간의 의존 관계를 자신이 아닌 외부 조립기가 수행
* 제어의 역행 (inversion of Control, IoC)라는 의미로 사용
* DI를 통해 시스템에 있는 각 객체를 조정하는 외부 개체가 객체들에게 생성시에 의존관계를 주어짐
* 느슨한 결합의 주요 강점
  * 객체는 인터페이스에 의한 의존 관계만을 알고 있으며, 이 의존 관계는 구현 클래스에 대한 차이를 모르는 채 서로 다른 구현으로 대체가 가능

<br>

---

<br>

## Spring 설정 : xml

* Application에서 사용할 Spring 자원들을 설정하는 파일
* Spring Container는 설정 파일에 설정된 내용을 읽어 Application에서 필요한 기능을 제공
* Root tag는 `<bean>`
* 파일명은 상관 없음

* 예 : applicationContext.xml

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
  	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
  
  	<bean id="kor" class="com.hello.HelloMessageKor"></bean>
  	<bean id="eng" class="com.hello.HelloMessageEng"></bean>
  
  </beans>
  ```

<br>

#### 기본 설정1 : 빈 객체 생성 및 주입

* 주입 할 객체를 설정 파일에 설정
  * `<bean>`
    * 스프링 컨테이너가 관리할 Bean 객체를 설정

* 기본 속성
  * `name` 
    * 주입 받을 곳에서 호출 할 이름 설정
    * 여러 객체에서 동일 값 가질 수 있음
  * `id`
    * 주입 받을 곳에서 호출 할 이름 설정
    * 유일 값
  * `class`
    * 주입 할 객체의 클래스
  * `factory-method`
    * Singleton 패턴으로 작성된 객체의 factory 메소드 호출
  * `scope`
    * singleton
    * prototype
  * 등등

*  예 : applicationContext.xml

  ```xml
  <bean id="kor" class="com.hello.HelloMessageKor"></bean>
  <bean id="eng" class="com.hello.HelloMessageEng"></bean>
  ```

<br>

#### 기본 설정2 : 빈 객체 얻기

* 설정 파일에 설정한 bean을 Container가 제공하는 주입기 역할의 api를 통해 주입 받음

* 예 : Java file

  ```java
  ApplicationContext context = new ClassPathXmlApplicationContext("com/hello/applicationContext.xml");
  
  HelloMessage korMessage = context.getBean("kor", HelloMessageKor.class);
  HelloMessage engMessage = context.getBean("eng", HelloMessageEng.class);
  ```

<br>

#### 스프링 빈 의존 관계 설정 - 방법1: Constructor 이용 

* 객체 또는 값을 생성자를 통해 주입 받는다

* `<constructor-arg>`

  * `<bean>`의 하위 태그로 설정한 bean 객체 또는 값을 생성자를 통해 주입하도록 설정

  * 설정 방법

    * `<ref>`, `<value>` 와 같은 하위 태그를 이용하여 설정하거나 또는 속성을 이용하여 설정

    1. 하위 태그 이용
       * 객체 주입 시 : `<ref bean="bean name"/>`
       * 문자열, primitive data 주입 시 : `<value>값</value>`
         * type 속성
           * 값은 기본적으로 String으로 처리
           * 값의 타입을 명시해야 하는 경우 사용
           * 예) `<value type="int">10</value>`

    2. 속성 이용
       * 객체 주입 시 : `<constructor-arg ref="bean name"/>`
       * 문자열, primitive data 주입 시 : `<constructor-arg value="값"/>`

<br>

#### 스프링 빈 의존 관계 설정 - 방법2 : Property 이용 

* Property를 통해 객체 또는 값을 주입 받는다

  * setter method
  * 주의 : setter를 통해서는 하나의 값만 받을 수 있음

* 일반적으로 사용하는 방법

* `<property>` 

  * `<bean>`의 하위태그로 설정한 bean 객체 또는 값을 property를 통해 주입하도록 설정

  * 설정 방법

    * `<ref>`, `<value>` 와 같은 하위 태그를 이용하여 설정하거나 또는 속성을 이용하여 설정 

    1. 하위 태그 이용
       * 객체 주입 시 : `<ref bean="bean name"/>`
       * 문자열, primitive data 주입 시 : `<value>값</value>`
    2. 속성 이용 : name - 값을 주입할 property 이름 (setter의 이름)
       * 객체 주입 시 : `<property name="propertyname" ref="bean name"/>`
       * 문자열, primitive data 주입 시 : `<property name="propertyname" value="값"/>`
    3. xml namespace를 이용하여 설정

  * 예시

    * 하위태그 이용

    ```xml
    <bean id="gbService" class="com.model.service.GuestBookServiceImpl">
    	<property name="guestBookDao">
    		<ref bean="gbDao"/>
    	</property> 
    </bean>
    ```

    * 속성 이용

    ```xml
    <bean id="gbService" class="com.model.service.GuestBookServiceImpl">
    		<property name="guestBookDao" ref="gbDao"/>
    </bean>
    ```

<br>

#### 스프링 빈 의존 관계 설정 - 방법3 : annotation 이용

* Annotation
  * 멤버 변수에 직접 정의 하는 경우 setter method를 만들지 않아도 됨

* `@Resource`
  * 멤버 변수, setter method에 사용 가능
  * 타입에 맞춰서 연결
* `@Autowired`
  * Spring에서만 사용 가능
  * Required 속성을 통해 DI 여부 조정
  * 멤버 변수, setter, constructor, 일반 method 사용 가능
  * 타입에 맞춰서 연결
* `@Inject`
  * Framework에 종속적이지 않음
  * Javax.inject-x.x.x.jar 필요
  * 멤버 변수, setter, constructor, 일반 method 사용 가능
  * 이름으로 연결
* 이름 새로 설정
  * `@XXX(value="name")`
*  이름을 통해 정확한 연결할 시
  * `@Qualifier("name")` / `@Qualifier("클래스이름의첫글자만소문자")`
  * 써주면 해당 이름을 가진 애로 연결됨

* 예시

  * Service.java

    ```java
    package com.model.service;
    
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.stereotype.Service;
    
    import com.model.dao.GuestBookDao;
    
    @Service(value = "gbService")
    public class GuestBookServiceImpl implements GuestBookService {
    	
    	@Autowired
    	private GuestBookDao guestBookDao;
    
    	...
    }
    ```

  * DAO.java

    ```java
    package com.model.dao;
    
    import javax.sql.DataSource;
    
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.stereotype.Repository;
    
    import com.model.GuestBookDto;
    import com.util.DBUtil;
    
    @Repository
    public class GuestBookDaoImpl implements GuestBookDao {
    
    	@Autowired
    	private DataSource dataSource;
    	
    	...
    }
    ```

  * applicationContext.xml

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <beans xmlns="http://www.springframework.org/schema/beans"
    	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    	xmlns:context="http://www.springframework.org/schema/context"
    	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
    		http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-4.3.xsd">
    
    <context:component-scan base-package="com.model"></context:component-scan>
    <beans ...>
    	...
    </beans>
    ```

<br>

#### Database Bean 설정

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:context="http://www.springframework.org/schema/context"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
		http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-4.3.xsd">

<beans ...>
	<bean id="gbDao" class="com.ssafy.model.dao.GuestBookDaoImpl">
		<property name="dataSource" ref="ds"/>
	</bean>
	<bean id="ds" class="org.springframework.jdbc.datasource.SimpleDriverDataSource">
		<property name="url" value="jdbc:mysql://127.0.0.1:3306/dbname?serverTimezone=UTC&amp;useUniCode=yes&amp;characterEncoding=UTF-8"/>
		<property name="driverClass" value="com.mysql.cj.jdbc.Driver"/>
		<property name="username" value="hereme"/>
		<property name="password" value="1111"/>
	</bean>
</beans>
```



