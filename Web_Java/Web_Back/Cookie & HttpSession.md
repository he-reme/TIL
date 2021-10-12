# Cookie & HttpSession

#### Session & Cookie

* HTTP protocol의 특징(약점)을 보완하기 위해 사용

* HTTP protocol 특징
  * client가 server에 요청
  * server는 요청에 대한 처리를 한 후 client에 응답
  * 응답 후 연결을 해제 (stateless)
    * 지속적인 연결로 인한 자원 낭비를 줄이기 위해 연결을 해제
    * 그러나 client와 server가 연결 상태를 유지해야 하는 경우 문제가 발생 (로그인 정보 등)
    * 즉 client 단위로 상태 정보를 유지해야 하는 경우 Cookie와 Session이 사용됨

<br>

---

<br>

## Cookie

> `javax.servlet.http.Cookie`

<br>

#### Cookie?

* 서버에서 사용자의 컴퓨터에 저장하는 정보 파일
* 사용자가 별도의 요청을 하지 않아도 브라우저는 request시 Request Header를 넣어 자동으로 서버에 전송
* key와 value로 구성되고 String 형태로 이루어져 있음
* Browser마다 저장되는 쿠키는 다름
  * 서버에서는 Browser가 다르면 다른 사용자로 인식

<br>

#### Cookie의 사용 목적

* 세션 관리
  * 사용자 아이디, 접속시간, 장바구니 등의 서버가 알아야 할 정보 저장
* 개인화
  * 사용자마다 다르게 그 사람에 적절한 페이지를 보여줄 수 있음
* 트래킹
  * 사용자의 행동과 패턴을 분석하고 기록

<br>

#### Cookie의 사용 예

* ID 저장 (자동 로그인)
* 일주일간 다시 보지 않기
* 최근 검색한 상품들을 광고에 추천
* 쇼핑몰 장바구니 기능

<br>

#### Cookie의 구성 요소

* 이름
  * 여러 개의 쿠키가 client의 컴퓨터에 파일 형태로 저장되므로 각 쿠키를 구별하는 데 사용되는 이름
* 값
  * 쿠키의 이름과 매핑되는 값
* 유효기간
  * 쿠키의 유효기간
* 도메인
  * 쿠키를 전송할 도메인
* 경로
  * 쿠키를 전송할 요청 경로

<br>

#### Cookie의 동작 순서

* Client가 페이지를 요청
* WAS는 Cookie를 생성
* HTTP Header에 Cookie를 넣어 응답
* Browser는 넘겨받은 Cookie를 PC에 저장하고, 다시 WAS가 요청할 때 요청과 함께 Cookie를 전송
* Browser가 종료되어도 Cookie의 만료 기간이 남아 있다면 Client가 계속 보관
* 동일 사이트 재방문시 Client의 PC에 해당 Cookie가 있는 경우, 요청 페이지와 함께 Cookie를 전송

<br>

#### Cookie의 특징

* 이름, 값, 만료일(저장 기간 설정), 경로 정보로 구성됨
* 클라이언트에 총 300개의 쿠키를 저장할 수 있음
* 하나의 도메인 당 20개의 쿠키를 가질 수 있음
* 하나의 쿠키는 4KB(=4096byte)까지 저장 가능

<br>

#### Cookie의 주요 기능

* 생성

  ```
  Cookie cookie = new Cookie(String name, String value);
  ```

* 값 변경 / 얻기

  ```
  cookie.setValue(String value);
  String value = cookie.getValue();
  ```

* 사용 도메인 지정 / 얻기

  ```
  cookie.setDomain(String domain);
  String domain = cookie.getDomain();
  ```

* 값 범위 지정 / 얻기

  ```
  cookie.setPath(String path);
  String path = cookie.getPath();
  ```

* cookie의 유효기간 지정 / 얻기

  ```
  cookie.setMaxAge(int expiry);
  int expiry = cookie.getMaxAge();
  ```
  * 쿠키 삭제

    ```
    cookie.setMaxAge(0);
    ```

* 생성된 cookie를 client에 전송

  ```
  response.addCookie(cookie);
  ```

* client에 저장된 cookie 얻기

  ```
  Cookie cookies[] = request.getCookies();
  ```

<br>

---

<br>

## Session

> `javax.servlet.http.HttpSession`

#### session?

* 방문자가 웹 서버에 접속해 있는 상태를 하나의 단위로 보고 그것을 세션이라고 함
* WAS의 memory에 Object의 형태로 저장
* memory가 허용하는 용량까지 제한 없이 저장 가능

<br>

#### session의 사용 예

* site내에서 화면을 이동해도 로그인(사용자 정보)이 풀리지 않고 유지
* 장바구니

<br>

#### session의 동작 순서

* 클라이언트가 페이지를 요청
* 서버는 접근한 클라이언트의 Request-Header 필드인 Cookie를 확인하여, 클라이언트가 해당 session-id를 보냈는지 확인
* session-id가 존재하지 않는다면, 서버는 session-id를 생성해 클라이언트에게 돌려준다
* 서버에게 클라이언트로 돌려준 session-id를 쿠키를 사용해 서버에 저장
  * 쿠키 이름 : JSESSIONID
* 클라이언트는 재 접속 시 이 쿠키(JSESSIONID)를 이용하여 session-id 값을 서버에 전달

<br>

#### Session의 특징

* 웹 서버에 웹 컨테이너의 상태를 유지하기 위한 정보를 저장
* 웹 서버에 저장되는 쿠키 (=세션 쿠키)
* 브라우저를 닫거나, 서버에서 세션을 삭제 했을 때만 삭제가 되므로, 쿠키보다 비교적 보안이 좋음
* 저장 데이터에 제한이 없음
* 각 클라이언트 고유 Session ID를 부여함
* Session ID로 클라이언트를 구분하여 각 클라이언트 요구에 맞는 서비스 제공

<br>

#### Session의 설정

* Browser당 하나의 JSESSIONID를 할당 받음
* 아이디 또는 닉네임과 같이 로그인 했을 경우 자주 사용되는 정보를 session에 저장하면 DB를 접근할 필요가 없으므로 효율적임

<br>

#### HttpSession의 주요 기능

* 생성

  ```java
  HttpSession session = request.getSession();
  HttpSession session = request.getSession(false); 
  ```

* 값 저장

  ```java
  session.setAttribute(String name, Object value);
  ```

* 값 얻기

  ```java
  Object obj = session.getAttribute(String name);
  ```

* 값 제거

  ```java
  session.removeAttribute(String name); // 특정 이름의 속성 제거
  session.invalidate(); // binding되어 있는 모든 속성 제거
  ```

* 생성 시간

  ```java
  long ct = session.getCreationTime();
  ```

* 마지막 접근 시간

  ```java
  long lat = session.getLastAccessedTime();
  ```

<br>

---

<br>

## Cookie & Session 정리

#### Cookie

* Type
  * Class
  * `javax.servlet.http.Cookie`
* 저장 위치
  * Client 컴퓨터에 file로 저장
* 저장 형식
  * file에 저장되기 때문에 String 형태
* 사용 예
  * 최근 본 상품 목록
  * 아이디 저장 (자동 로그인)
  * 팝업 메뉴에서 '오늘은 그만 열기' 등
* 용량 제한
  * 도메인당 20개
  * 1쿠키당 4KB
* 만료 시점
  * 쿠키 저장 시 설정
  * 설정이 없을 경우
    * Browser 종료 시

<br>

#### Session

* Type
  * Interface
  * `javax.servlet.http.HttpSession` 
* 저장 위치
  * Server의 memory에 Object로 저장
* 저장 형식
  * Object는 모두 가능
  * 일반적으로 Dto, List 등 저장
* 사용 예
  * 로그인 시 사용자 정보
  * 장바구니 등
* 용량 제한
  * 제한 없음
* 만료 시점
  * 알 수 없음
  * Client가 로그아웃을 하거나, 일정 시간동안 session에 접근 하지 않을 경우
  * 만료 시간은 `web.xml`에 설정

<br>

#### 공통

* 전역에 저장하기 때문에 project 내의 모든 JSP에서 사용 가능
* Map 형식으로 관리하기 때문에 key 값의 중복을 허용하지 않음