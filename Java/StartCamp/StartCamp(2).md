# Start Camp (2)

> web 기초

<br>

---

<br>

## `.class` 실행했을 때

#### Stack

* 변수 저장

<br>

#### Heap

* `new` 로 생성된 것, `heap` 메모리 영역에 올라감
* Garbage Collector가 메모리 관리해줌
* 예) 배열

<br>

#### Static

* `Java.lang.Math`
* `Java.lang.System`
* `Main` 함수

<br>

#### 코드표

* 문자열 저장 (new로 생성안했을 때)
  * 문자열은 new로 생성하는 거 보다 안쓰는 걸 추천
  * 하나의 문자열을 한번만 생성, 사용하기 때문에 메모리를 상대적으로 덜 사용

<br>

---

<br>

## Web 폴더 구조

#### 계층 구조

* board
  * html, jsp, css, js,  Image
  * WEB-INF
    * Classes
    * lib
    * web.xml
    * src
    * tld

<br>

#### board

* WebContent 폴더

#### html, jsp, css, js,  Image

* **Client가 직접 access 가능**
* `http` 로 지정되어있을 때 모든 사람에게 **open** !

<br>

#### WEB-INF

* **보안 폴더**
* **continer, JVM만 접근 가능**

<br>

#### classes

* 패키지형태 클래스 파일 (서블릿 클래스, 빈즈 클래스)

<br>

#### lib

* jar 형태로 참조하는 외부 라이브러리 위치

<br>

#### web.xml

* Listener, Filter, Servlet, 전역세션, 리소스 관리
* 웹이 돌아갈 때 전반적인 환경 설정 파일

<br>

#### src, tld

* 필요한 경우 option

<br>

---

<br>

## Tomcat Server 실행하기

1. 프로젝트 폴더 마우스 우클릭

2. `Run As`  클릭
3. `Run On Server` 클릭

4. Tomcat 선택하고 Next
5. Configured 에서 프로젝트명 확인하고
6. finish !!

<br>

---

<br>

## HTML

#### form

* post
  * 보내는 데이터의 길이 제한 없음
  * reload(새로고침) 안됨
  * 노출 안됨
* get

