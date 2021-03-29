# Selenium

> 웹 브라우저를 자동화 하는 도구 모음
>
> 동적 스크래핑에 사용

* WebDriver 라는 API를 통해 운영체제에 설치된 크롬이나 파이어폭스 등의 브라우저를 기동시키고 웹 페이지를 로드하고 제어
* 브라우저를 직접 동작시킨다는 것
  * JavaScript에 의해 생성되는 콘텐츠와 Ajax 통신 등을 통해 뒤늦게 불려오는 콘텐츠를 처리할 수 있다는 것을 의미

#### WebDriver API

* 간결한 프로그래밍 인터페이스를 제공하도록 설계
* 동적 웹페이지를 보다 잘 지원할 수 있도록 개발
* 목표 
  * 최신 고급 웹 응용 프로그램 테스트 문제에 대한 향상된 지원을 제공하는 잘 디자인된 객체지향 API를 제공하는 것
* `Selenium-WebDriver`는 자동화를 위한 각 브라우저의 기본 지원을 사용하여 브라우저를 직접 호출

#### Selenium 설치

* cmd창에서 pip명령 또는 conda 명령을 통해 설치 가능

```shell
conda install selenium
pip install selenium
```

#### 임포트 패키지

```python
from selenium import webdriver
```



---



## 객체 생성 및 페이지 가져오기

#### WebDriver 객체 생성

* 크롬 드라이버를 기반으로`selenium.webdriver.chrome.webdriver.WebDriver` 객체 생성

  ```python
  driver = webdriver.Chrome('C:/Temp/chromedriver')
  ```
  * 아규먼트로 `chromedriver.exe` 파일이 존재하는 디렉토리와 파일명에 대한 패스 정보를 지정하면 Selenium에 의해 관리되는 크롬 브라우저가 기동 됨
  * 드라이버 종료
    * `driver.quit()`
    * 수행 후 바로 꺼져버리기 때문에 굳이 사용 안하고 싶으면 사용 안해도 됨

#### 페이지 가져오기

* `selenium.webdriver.chrome.webdriver.WebDriver` 객체의 `get()` 메서드를 사용하여 크롤링하려는 웹 페이지를 제어하는 크롬 브라우저에 로드하고 렌더링

  ```python
  driver.get('크롤링하려는웹페이지URL')
  ```

* 경우에 따라서 페이지 로드가 완료되거나 시작되기 전에 WebDriver가 제어권을 반환할 수 있음

* 견고성을 확보하려면 Explicit and Implicit Waits를 사용하여 요소가 페이지에 존재할 때까지 기다려야 함

  ```python
  # 방법1
  driver.implicitly_wait(3)
  driver.get('크롤링하려는웹페이지URL')
  ```

  ```python
  # 방법2
  driver.get('크롤링하려는웹페이지URL', 5)
  ```



---



## 요소 찾기

> WebDriver의 요소 찾기는 WebDriver 객체 및 WebElement 객체에서 제공되는 다음 메서드들을 사용

#### 조건에 맞는 요소 한개 찾기 : WebElement 객체 리턴

```python
driver.find_element_by_XXX("XXX에 알맞은 식")
```

#### 조건에 맞는 모든 요소 찾기 : list 객체 리턴

```python
driver.find_elements_by_XXX("XXX에 알맞은 식")
```

* 태그의 id 속성 값으로 찾기

  ```python
  target = driver.find_element_by_id('Id명')
  ```

* 태그의 class 속성 값으로 찾기

  ```python
  target = driver.find_element_by_class_name('클래스명')
  ```

* 태그명으로 찾기

  ```python
  target = driver.find_element_by_tag_name('h1')
  ```

* 링크 텍스트로 태그 찾기 (`a태그`의 컨텐트로 찾기)

  `<a href="https:www.python.org/">파이썬 학습 사이트</a>`

  ```python
  target = driver.find_element_by_link_text('파이썬 학습 사이트')
  ```

* 부분 링크 텍스트로 태그 찾기

  ```python
  target = driver.find_element_by_partial_link_text('사이트')
  ```

* CSS 선택자로 태그 찾기

  ```python
  target = driver.find_element_by_css_selector('CSS선택자')
  ```

* Xpath로 태그 찾기

  ```python
  target = driver.find_element_by_xpath('Xpath')
  ```



---



## 찾은 객체 다루기

* input 태그

  ```python
  from selenium.webdriver.common.keys import keys
  target.send_keys('입력할단어')
  target.send_keys(Keys.Enter)
  ```

* 태그명 추출

  ```python
  target.tag_name
  ```

* 텍스트 형식의 콘텐츠

  ```python
  target.text
  ```

* 속성값

  ```python
  target.get_attribute('속성명')
  ```

* 클릭 이벤트

  ```python
  import time # 파이썬 time 패키지
  target.click()
  time.sleep(1)
  ```

  * `click()` 이후엔 시간 조금 주기

* txt 파일로 저장

  ```python
  wfile = open("원하는이름.txt","w", encoding="utf-8") 
  wfile.writelines(저장할데이터변수) 
  wfile.close()
  ```

  

---



## 예시

* google 입력창에 '파이썬' 입력

  ```python
  from selenium import webdriver
  from selenium.webdriver.common.keys import Keys 
  
  driver = webdriver.Chrome('C:/Temp/chromedriver') # 크롬 드랄이버 위치
  print("WebDriver 객체 : ", type(driver))
  
  driver.get('http://www.google.com/ncr') 
  target=driver.find_element_by_css_selector("[name = 'q']")
  print("찾아온 태그 객체 : ", type(target))
  target.send_keys('파이썬')
  target.send_keys(Keys.ENTER)
  ```

* 네이버 호텔 댓글 스크래핑

  ```python
  from selenium import webdriver
  import time
  
  driver = webdriver.Chrome('C:/Temp/chromedriver', 3)
  url = "https://hotel.naver.com/hotels/item?hotelId=hotel:Shilla_Stay_Yeoksam&destination_kor=%EC%8B%A0%EB%9D%BC%EC%8A%A4%ED%85%8C%EC%9D%B4%20%EC%97%AD%EC%82%BC&rooms=2"
  driver.get(url)
  time.sleep(5)
  tabButton = driver.find_element_by_css_selector('div.container.ng-scope > div.content > div.hotel_used_review.ng-isolate-scope > ul > li.ng-scope.item_ta > a')
  tabButton.click()
  time.sleep(2)
  reviewList = []
  while True :
      reviews = driver.find_elements_by_css_selector('div.hotel_used_review.ng-isolate-scope > div.review_ta.ng-scope > ul > li > div.review_desc > p')
      for review in reviews :
          reviewList.append(review.text)
      nextButton = driver.find_element_by_css_selector('div.hotel_used_review.ng-isolate-scope > div.review_ta.ng-scope > div.paginate > a.direction.next')
      if nextButton.get_attribute('class') == "direction next disabled" :
          break
      nextButton.click()
      time.sleep(2)
      
  print(len(reviewList))
  wfile = open("C:/KHR/PYDATAexam/output/naverhotel.txt","w", encoding="utf-8") 
  wfile.writelines(reviewList) 
  wfile.close()
  ```

* 스크래핑할 프레임 바꾸고, 스크롤

  ```python
  #소스2 : 스크롤
  from selenium import webdriver
  from selenium.webdriver.common.keys import Keys 
  
  driver = webdriver.Chrome('C:/Temp/chromedriver')
  driver.implicitly_wait(3) 
  driver.get('https://map.naver.com/') 
  import time
  time.sleep(2)
  
  target=driver.find_element_by_css_selector(".input_search")
  
  target.send_keys('서울시어린이도서관')
  target.send_keys(Keys.ENTER)
  
  time.sleep(2)
  # iframe 태그를 사용해서 구성된 페이지 (페이지 안에 다른 프레임) 스크래핑 할 때 switch 해야 함
  driver.switch_to.frame("searchIframe")
  while True :
      count = 9
      while True :
          print("스크롤 : " +str(count))
          try :
              driver.execute_script("var su = arguments[0]; var dom=document.querySelectorAll('#_pcmap_list_scroll_container>ul>li')[su]; dom.scrollIntoView();", count)
              time.sleep(2)
          except :        
              break
          count += 10
      names = driver.find_elements_by_css_selector("span._16f7Q")
      addrs = driver.find_elements_by_css_selector("span._3W_ec")
      if len(names) == 0 :
          print("추출되는 도서관이 더 이상 없음")
          break
      for i in range(len(names)) :
          print(names[i].text,addrs[i].text, sep=", ", end="\n")
      print("------------------------------------------------")
      linkurl = '#app-root > div > div > div._2ky45 > a:nth-child(7)'
      try :
          linkNum = driver.find_element_by_css_selector(linkurl)
      except :
          print("더 이상 다음 페이지 없음")
          break
      linkNum.click()  
      time.sleep(5)
  print("스크래핑 종료")
  
  #driver.quit()
  ```

  
