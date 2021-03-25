# `request` 패키지

> `requests` 패키지를 활용한 웹 페이지 요청
>
> `urllib` 에서 확장?

* HTTP 프로토콜과 관련된 기능 지원

* 파이썬 라이브러리
  * 아나콘다에는 `requests` 패키지가 `site-packages`로 설치되어있음
  * 만일 설치해야한다면 다음 명령으로 설치
    * `conda install requests`
    * `pip install requests`

#### import

```python
import requests
```



#### HTTP Response 객체 구성

* Header : 응답상태코드, 응답 메세지
  * name : value로 구성되는 여러 정보들
  * 등등

* Body : HTML 전체 내용
  * `<html>~</html>`



---



## `requests.request()`

* `requests` 패키지의 대표 함수
* HTTP 요청을 서버에 보내고 응답을 받아오는 기능 지원

#### `urllib` 패키지 vs `requests` 패키지

* `urllib`
  * 인코딩하여 바이너리 형태로 데이터 전송
  * 요청 방식 (GET, POST)에 따라서 구현 방법이 달라짐
* `requests`
  * 딕셔너리 형태로 데이터 전송
  * `request()` 함수 호출 시 요청 메소드 (GET, POST)를 명시하여 요청

#### `requests.request(method, url, **kwargs)`

* method
  * 요청 방식 지정
  * GET, POST
    * HTTP Response Header, Body 둘 다 받아옴
  * HEAD
    * HTTP Response Header만 받아옴
  * PUT, DELETE, OPTIONS
* url
  * 요청할 대상 URL 문자열 지정
* params 
  * 선택적
  * 요청 시 전달할 Query 문자열 지정
  * 딕셔너리, 튜플리스트, 바이트열 가능
* data
  * 선택적
  * 요청 시 바디에 담아서 전달할 요청 파라미터 지정
  * 딕셔너리, 튜플리스트, 바이트열 가능
* json
  * 선택적
  * 요청 시 바디에 담아서 전달할 JSON 타입의 객체 지정
* auth
  * 선택적
  * 인증처리(로그인)에 사용할 튜플 지정



---



#### 요청 방식 지정

* ` requests.request()` 함수에 요청 방식을 지정하여 호출하는 것과 아래의 함수들은 동일

  * `request.get(url, params=None, **kwargs)`
  * `requests.post(url, data=None, json=None, **kwargs)`
  * `requests.head(url, **kwargs)`
  * `requests.put(url, data=None, **kwargs)`
  * `requests.patch(url, data=None, **kwargs)`
  * `requests.delete(url, **kwargs)`

* GET 방식 요청 (2가지 방법)

  ```python
  requests.request('GET', url, **kwargs) # 방법1
  requests.get(url, params=None/원하는거, **kwargs) # 방법2
  ```

  * Query 문자열을 포함하여 요청
    * `params 매개변수`에 딕셔너리, 튜플리스트,  바이트열 형식으로 전달
  * Query 문자열을 포함하지 않는 요청
    * `params 매개변수`의 설정 생략

* POST 방식 요청 (2가지 방법)

  ```python
  requests.request('POST', url, **kwargs) # 방법1
  requests.post(url, params=None/원하는거, **kwargs) # 방법2
  ```

  * `data 매개변수`나 `json 매개변수`로 요청 파라미터를 지정하여 요청하는 것이 일반적
    * `data 매개변수` [선택적]
      * 딕셔너리, 튜플리스트 형식, 바이트열 형식으로 지정
    * `json 매개변수` [선택적]
      * JSON 객체 형식 지정



---



#### 리턴값 : `requests.models.Response 객체`

* `requests.request()`, `requests.get()`,`requests.head()`, `requests.post()` 함수의 리턴값

* Text

  * **문자열 형식**으로 응답 콘텐츠 추출

  * 추출 시 사용되는 문자 셋은 `ISO-8859-1` 이므로

  * `utf-8`이나 `euc-kr` 문자 셋으로 작성된 콘텐츠 추출 시 한글이 꺠지는 현상 발생 

  * 추출 전 응답되는 콘텐츠의 문자 셋 정보를 읽고 `r.encoding='utf-8'`와 같이 설정한 후 추출

    * `r` 은 리턴값을 담은 변수

  * 사용 

    ```python
    r = requests.request('get', 'URL')
    r.encoding = 'utf-8'
    print(r.text)
    ```

* Content

  * **바이트열 형식** 으로 응답 콘텐츠 추출
  * 응답 콘텐츠가 이미지와 같은 **바이너리 형식**인 경우 사용
  * 한글이 들어간 문자열 형식인 경우 `r.content.decode('utf-8')`를 사용해서 디코드 해야 함)

  * 사용

    ```python
    r = requests.request('get', 'URL')
    print(r.content.decode('utf-8'))
    print(r.content)) # 한글 깨짐
    ```

* url

  ```python
  r = requests.request('get', 'URL')
  print(r.url) # URL
  ```



---



### 이미지, 바이너리 저장

```python
import requests
from PIL import Image
from io import BytesIO

r = requests.get('http://unico2013.dothome.co.kr/image/flower.jpg')
i = Image.open(BytesIO(r.content))
i.save("c:/Temp/test.jpg")
```



---



## 예시

* 쿼리문을 포함한 url 전송 후 body 출력 (1)

```python
import requests
dicdata = {'category': '여행', 'page':100}
url = "http://unico2013.dothome.co.kr/crawling/exercise.php"
r = requests.request('GET', url, params=dicdata)
r.encoding = 'utf-8'
print(r.text)
```

쿼리문을 포함한 url 전송 후 body 출력 (2)

```python
import requests
dicdata = {'category': '여행', 'page':100}
url = "http://unico2013.dothome.co.kr/crawling/exercise.php"
r = requests.get(url, params=dicdata)
r.encoding = 'utf-8'
print(r.text)
```

