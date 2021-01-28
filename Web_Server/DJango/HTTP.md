# HTTP

> Hypertext transfer Protocol
>
> 프로토콜(통신규약)

* 상태가 없는 프로토콜

  * 데이터를 주고 받기 위한 각각의 데이터 요청이 서로 독립적으로 관리됨

  * 쉽게 말해서, 이전 데이터 요청과 다음 데이터 요청이 서로 관련이 없다는 것

* 일반적으로 TCP/IP 통신 위에서 동작

* 기본포트는 **80**번



---



## HTTP Request / HTTP Response

* HTTP 프로토콜로 데이터를 주고받기 위해서는
  * 클라이어트가 요청(request)을 보내고
  * 서버가 응답을(response)를 받아야 한다.



---



## URL

> Uniform Resource Locators

* 서버에 자원을 요청하기 위해 입력하는 영문 주소
* `http://www.domain.com:1234/path/to/resource?a=b&x=y`
  * `http` : protocol
  * `www.domain.com` : host
  * `1234` : port
  * `path/to/resource` : resource path
    * 생략되면 **기본 파일 (index.html)**을 달라는 의미로 해석됨
  * `?a=b&x=y` : query



---



## HTTP 요청 메서드

* URL을 이용하면 서버에 특정 데이터를 요청할 수 있는데
* 요청하는 데이터에 특정 동작을 수행하고 싶을 경우엔
* **HTTP 요청 메서드 (Http Request Methods)**를 이용
* GET이 기본

#### GET

존재하는 자원에 대한 요청

#### POST

새로운 자원을 생성

#### PUT

존재하는 자원에 대한 변경

#### DELETE

존재하는 자원에 대한 삭제



---



## HTTP 상태 코드

* 브라우저는 서버에 HTTP Request (URl + 요청 메서드) 를 보내고
* 서버는 브라우저에 HTTP Response (상태코드 + 응답 Body) 를 보낸다.

#### 2XX : 성공

#### 3XX : 리다이렉션

#### 4XX : 클라이언트 에러

#### 5XX : 서버 에러



