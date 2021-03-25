# `urllib` 패키지

> `urllib` 패키지를 활용한 웹페이지 요청

* URL 관련 라이브러리라는 의미의 패키지
* 파이썬의 표준 라이브러리

#### import

```python
from urllib.request
from urllib.parse
```

* 필요한거 선택

#### URL 문자열과 웹 요청에 관련된 모듈 5개 제공

* `urllib.request` ★
  * URL 문자열을 가지고 **요청 기능** 제공
* `urllib.response` ★
  * urllib 모듈에 의해 사용되는 **응답** 기능 관련 클래스들 제공
* `urllib.parse` ★
  * URL 문자열을 **파싱하여 해석**하는 기능 제공
* `urllib.error`
  * `urllib.request`에 의해 발생하는 예외 클래스들 제공
* `urllib.robotparser`
  * `robots.txt` 파일을 구문 분석하는 기능 제공



---



## `urllib.request` 모듈

>  URL 문자열을 가지고 **요청 기능** 제공
>
> URL 문자열을 가지고 HTTP 요청을 수행하는 모듈

* `urlopen()` 함수를 사용하여 웹 서버에 페이지를 요청

* 서버로부터 받은 응답을 저장하여 **응답 객체 (`http.client.HTTPResponse`)** 를 반환

  ```python
  res = urllib.request.urlopen("요청하려는 페이지의 URL 문자열")
  ```

####  `http.client.HTTPResponse` 객체

* 웹 서버로부터 받은 응답을 래핑하는 객체
* 응답 헤더나 응답 바디의 내용을 추출하는 메서드 제공
* `HTTPResponse.read()` ★
* `HTTPResponse.getheaders()`
* `HTTPResponse.msg`
* `HTTPResponse.version`
* `HTTPResponse.status`

#### `HTTPResponse.read()`

* 웹 서버가 전달한 데이터(**응답바디**)를 **바이트 열**로 읽어들임

  * 바이트 열 : 16진수로 이루어진 수열
    * 읽기 어려워서 웹 서버가 보낸 한글을 포함한 텍스트 형식의 HTML 문서의 내용을 읽을 때는 텍스트 형식으로 변환하기 때문에
    * 바이트열 객체의 `decode('문자셋')` 메서드를 실행하여 응답된 문자셋에 알맞은 문자열로 변환해야 함
    * 한글을 잘 읽어들이고 싶으면 `res.read().decode('utf-8')` 로 사용!!

* `res.read(index).decode('utf-8')`

  * `index`를 지정해서 원하는 길이만큼 읽어들일 수 있음
  * `res` 는 응답 객체를 담고 있는 변수

* 웹 페이지 인코딩 체크!

  * 웹 크롤링 하려는 웹 페이지가 어떠한 문자 셋으로 작성 되어있는지 파악하는 것 필수 (방법2)

    1. 페이지 소스 내용에서 `<meta>` 태그의 `charset` 정보 확인

    2. 파이썬 프로그램으로 파악 가능

       ```
       url = "원하는 URL"
       f = urllib.request.urlopen(url)
       encoding = f.info().get_content_charset()
       ```

       * `http.client.HTTPMessage` 객체의 `get_content_charset()` 메서드 사용
       * `urllib.request.rulopen()` 함수의 리턴값인 `http.client.HTTPResponse` 객체의 `info()` 메서드 호출하면, `http.client.HTTPMessage` 객체가 리턴됨



---



## `urllib.parse` 모듈

>  URL 문자열을 **파싱하여 해석**하는 기능 제공
>
> URL 문자열(주소)을 해석하는 모듈

* 웹 서버 페이지 또는 정보를 요청할 때 함께 전달하는 데이터
  * `name=value&name=value&name=value&...`
  * GET 방식 요청 : Query 문자열
    * URL 문자열과 관련 있음
  * POST 방식 요청 : 요청 파라미터
    * URL 문자열과 관련 없음

* 영문과 숫자는 그대로 전달되지만, 한글은 `%`기호와 함께 16진수 코드 값으로 전달되어야 함
* 웹 크롤링을 할 때 요구되는 Queary 문자열을 함께 전달해야 하는 경우, 직접 Query 문자열을 구성해서 전달해야 함

### `urllib.parse` 모듈 사용

* `urllib.parse.urlparse()`
* `urllib.parse.urlencode()`



---



#### `urllib.parse.urlparse("URL문자열")`

> 객체 정보 추출하기

* 아규먼트에 지정된 URL 문자열의 정보를 다음과 같이 구성하여 저장하는 `urllib.parse.ParseResult` 객체를 리턴함

  ```
  url = urlparse("https://movie.daum.net/moviedb/main?movieId=93252")
  ```

  * 리턴된 `urllib.parse.ParsResult` 객체 정보

    ```
    ParseResult(scheme="https", netloc="movie.daum.net",
    			path="/moviedb/main", params="",
    			query="movieId=93252", fragment="")
    ```

* 각 속성들을 이용하여 필요한 정보만을 추출할 수 있음

  * `url.netloc`
  * `url.path`
  * `url.query`
  * `url.scheme`
  * `url.port`
  * `url.fragment`
  * `url.geturl()`



---



#### `urlllib.parse.urlencode()`

> **원하는 url로 만들어주기 위한 함수.** 쿼리 문자열을 만들어줌

* 메서드의 아규먼트로 지정된 name과 value로 구성된 **딕셔너리 정보**를

* 정해진 규격의 **Query 문자열 또는 요청 파라미터 문자열로 리턴**함

* 예시1

  ```
  urlencode({'number':12524, 'type':'issue', 'action':'show'})
  ```

  * 리턴된 Query 문자열 또는 요청 파라미터 문자열

    ```
    number=12524&type=issue&action=show
    ```

* 예시2 - 한글이 포함되어 있을 때

  ```
  urlencode({'addr': '서울시 강남구 역삼동'})
  ```

  * 리턴된 Query 문자열 또는 요청 파라미터 문자열 

    ```
    addr = %EC%84%9C.....
    ```

#### GET 방식 요청

* Query 문자열을 포함하여 요청하는 것

* 과정

  1. `urllib.parse.urlencode` 함수로 `name`과 `value`로 구성되는 Query 문자열을 만듦
  2. 이 Query 문자열을 URL 문자열 뒤에 `?%s` 기호 추가하여 요청 URL로 사용

* 예시

  ```python
  params = urllib.parse.urlencode({'name': '김혜림', 'age': '25'})
  url = "URL문자열?%s" % params
  urllib.request.urlopen(url)
  ```

#### POST 방식 요청

* 요청 바디 안에 요청 파라미터를 포함하여 요청하는 것

* 과정

  1. GET 방식과 같이 `urllib.parse.urlencode` 함수로 `name`과 `value`로 구성되는 Query 문자열을 만듦
  2. POST 방식 요청에서는 바이트 형식의 문자열로 전달해야 하므로 `encode('ascii')` 메서드를 호출하여 바이트 형식의 문자열로 변경
  3. `urllib.request.urlopen()` 호출 시 바이트 형식의 문자열로 변경된 데이터를 두 번째 아규먼트로 지정!
     * 혹은... `urllib.request.Request` 객체를 지정하는 방법이 있음

* 예시1 - 첫번째 방법

  ```python
  data = urllib.parse.urlencode({'name': '김혜림', 'age': '25'})
  postdata = data.encode('ascii')
  url = "URL문자열"
  urllib.request.urlopen(url, postdata)
  ```

* 예시2 - 두번째 방법

  ```R
  data = urllib.parse.urlencode({'name': '김혜림', 'age': '25'})
  postdata = data.encode('ascii')
  req = urllib.request.Request(url="URL문자열", data=postdata)
  urllib.request.urlopen(req)
  ```




---



## 예시

* 쿼리문을 포함한 url 전송 후 body 출력

 ```python
import urllib.request
import urllib.parse
params = urllib.parse.urlencode({'category': '역사', 'page':25})
url = "http://unico2013.dothome.co.kr/crawling/exercise.php?%s" % params
r = urllib.request.urlopen(url)
print(r.read().decode('utf-8'))
 ```

