# Open API

* API

  * `Application Programming Interface`

  * 특정 프로그램을 만들기 위해 제공되는 모듈 (함수 등)
  * `Client` > `API` > `DB` > `DB Data`



---



#### Open API

* 공개 API
* 누구나 사용할 수 있도록 공개된 API
* 주로 **Rest API** 기술을 많이 사용
  * 웹에서 사용하는 API

#### Rest API

* `Representational State Transfer API`
* HTTP 프로토콜을 통해서 정보를 제공하는 함수
* 실질적인 API 사용은 **정해진 구조의 URL 문자열 사용**

* 일반적으로 `XML`, `JSON` 형태로 응답 출력



---



## xml, json 형태로 파일 저장

`exam3` 확인



---



## 네이버 Open API 사용하기

#### 네이버 지역 서비스

* 참고 문서

  `https://developers.naver.com/docs/serviceapi/search/local/local.md#%EC%A7%80%EC%97%AD`

* 코드

  ```python
  import urllib.request
  from bs4 import BeautifulSoup
  import json
  
  def naver_search(keyword, callType='JSON') :
      # 발급 받은 키
      client_key = '사용하려면 발급 받기'
      client_secret = '사용하려면 발급 받기'
      
      # 요청 url
      base = 'https://openapi.naver.com/v1/search'
      node = '/local'
      parameters = '?query=' + urllib.parse.quote_plus(keyword) + '&display=5'
      
      if callType=='XML' :
          node = node + '.xml'
      elif callType=='JSON' :
          node = node + '.json'
  
      url = base + node + parameters
      
      # 요청 url에 헤더 포함시키기
      request = urllib.request.Request(url)
      request.add_header("X-Naver-Client-Id",client_key)
      request.add_header("X-Naver-Client-Secret",client_secret)
      
      # 요청한 코드 받아서 열기
      response = urllib.request.urlopen(request)
      rescode = response.getcode()
      response_body = response.read()
      
      # 반환된 code가 200이어야 정상 작동된 것
      if rescode != 200 :
          print('오류 코드 : ' + rescode)
          return
      
      if callType=='XML' :
          soup = BeautifulSoup(response_body.decode('utf-8'), 'xml')
          # print(soup) # 구조 확인하기
          print('[짜장면집에 대한 네이버 지역 정보(XML)]')
          index = 1
          for item in soup.find_all('item') :
              title = item.find('title').string
              address = item.find('address').string
              print(f"{index} : {title}, {address}")
              index = index + 1
              
      elif callType=='JSON' :
          dataList = json.loads(response_body)
          # print(dataList) # 구조 확인하기
          print('[쌀국수집에 대한 네이버 지역 정보(JSON)]')
          index = 1
          for item in dataList['items'] :
              title = item['title']
              address = item['address']
              print(f"{index} : {title}, {address}")
              index = index + 1
  ```

* 실행 및 결과 1

  ```python
  naver_search('짜장면', 'XML')
  ```

  ```
  [짜장면집에 대한 네이버 지역 정보(XML)]
  1 : 딘타이펑 명동점, 서울특별시 중구 명동1가 59-1
  2 : 몽중헌 페럼타워점, 서울특별시 중구 수하동 66
  3 : 원흥, 서울특별시 중구 다동 92
  4 : 복성각 덕수궁점, 서울특별시 중구 태평로2가 366-1 오천회관빌딩 2층
  5 : 더 플라자 도원, 서울특별시 중구 태평로2가 23
  ```

* 실행 및 결과 2

  ```python
  naver_search('쌀국수')
  ```

  ```
  [쌀국수집에 대한 네이버 지역 정보(JSON)]
  1 : 포하노이, 서울특별시 종로구 청진동 70 B1
  2 : 호아빈 서울시청점, 서울특별시 중구 서소문동 14-2
  3 : 미스사이공 명동, 서울특별시 중구 명동2가 54-2
  4 : 반포식스 광화문점, 서울특별시 종로구 신문로1가 239
  5 : 사이공, 서울특별시 종로구 종로1가 24
  ```

  