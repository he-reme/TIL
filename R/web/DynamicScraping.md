# 동적 스크래핑

#### 동적 웹페이지

* 사용자의 선택과 같은 이벤트에 의해서 자바스크립트의 수행 결과로 컨텐츠를 생성한다
* 페이지의 렌더링을 끝낸 후에 Ajax 기술을 이용하여 서버로부터 컨텐츠의 일부를 전송받아 동적으로 구성한다

* 따라서 동적 웹페이지 스크래핑 하기 위해서는 Selenium 서버 필요



---



## Selenium

* 이를 사용하면 제어되는 브라우저에 페이지를 렌더링 해놓고 렌더링된 결과에서 컨텐츠를 읽어올 수 있다
* 뿐만 아니라 컨텐츠 내에서 클릭 이벤트를 생성할 수 있으며
* 로그인과 같은 데이터를 입력화 하는 것도 가능하다

#### Selenium 서버 기동 과정

1. `jdk` 설치 및 환경변수 설정

2. `chromedriver.exe` , `selenium-server-standalone-4.0.0-alpha-1.jar` 같은 폴더에 저장

3. [cmd] 해당 폴더 내에서 아래의 명령 수행 하여 Selenium 서버 기동

   `java -Dwebdriver.chrome.driver="chromedriver.exe" -jar selenium-server-standalone-4.0.0-alpha-1.jar -port 4445`

#### 제대로 기동 됐는지 확인하기

* 테스트 환경 : RStudio
* 크롬 : 최신 버전
* `install.packages("Rselenium")`
* `library(Rselenium)`

```R
install.packages("RSelenium") # 최초 한번만 설치
library(RSelenium) # 패키지 실행

# Selenium 서버에 접속
remDr <- remoteDriver(remoteServerAddr = "localhost" , port = 4445, browserName = "chrome") 

# Selenium 서버에 의해 제어되는 브라우저 기동
remDr$open()

# 지정된 URL 페이지를 요청하고 랜더링(자바스크립트코드 수행)
remDr$navigate("http://www.google.com/")

# 태그에 대한 DOM 객체 찾기
webElem <- remDr$findElement(using = "css selector", "[name = 'q']")

# <input> 태그에 텍스트를 입력하고 엔터키 입력을 자동화 하기
webElem$sendKeysToElement(list("PYTHON", key = "enter"))
```



---



## API

#### 기본

* R 코드로 Selenium 서버에 접속하고 remoteDriver 객체 리턴

  ```R
  remDr <- remoteDriver(remoteServerAddr="localhost", port=4445, browserName="chrome")
  ```

* 브라우저 오픈(크롬)

  ```R
  remDr$open()
  ```

* url에 해당하는 웹페이지 랜더링

  ```R
  remDr$navigate(url)
  ```

#### 태그 찾기 

* 한 개 찾기. 해당 태그가 없으면 `NoSuchElement` 오류 발생 - `WebElement 객체` (노드 한 개) 리턴

  ```R
  one <- remDr$findElement(using='css selector', 'css 선택자')
  ```

* 여러 개 찾기. 해당 태그가 없어도 오류 없이 빈 리스트 반환  - `WebElemnt 리스트 객체` 리턴 

  ```R
  more <- remDr$findElements(using='css selector', 'css 선택자')
  ```

#### 한 개의 태그

* 찾아진 태그의 태그 명 추출

  ```R
  one$getElementTagName()
  ```

* 찾아진 태그의 내용(컨텐츠) 추출

  ```R
  one$getElementText()
  ```

* 찾아진 태그의 속성 명에 대한 값 추출

  ```R
  one$getElementAttribute("속성명")
  ```

* 찾아진 태그에서 클릭이벤트 발생시키기

  ```R
  one$clickElement()
  ```

#### 여러 개의 태그

* 찾아진 태그들의 내용(컨텐츠) 추출

  ```R
  sapply(more, function(x){ x$getElementText() })
  ```

* 찾아진 태그들에 각각 클릭 이벤트 발생시키기

  ```R
  sapply(more, function(x){ x$clickElement(0) })
  ```
  * 가끔... `clickElement()`가 일을 안할 때

    ```R
    remDr$executeScript("arguments[0].click();", nextPageLink)
    ```

    ```R
    # 예시 코드
    url <- "http://unico2013.dothome.co.kr/crawling/exercise_bs.html"
    remDr$navigate(url)
    
    # href 속성값으로 "http://www.python.org/" 를 가진 a 태그
    one<-remDr$findElement(using='css selector','a:nth-of-type(3)')
    one$getElementTagName()
    one$getElementText()
    remDr$executeScript("arguments[0].click();",list(one));
    ```

* 페이지를 아래로 내리는(스크롤) 효과

  * 대부분 스크롤 안해도 되지만 

  * 특정 웹페이지는 해당 데이터 위치로 스크롤을 해야 데이터를 정상적으로 읽을 수 있음.

  * body 태그의 스크롤

    ```R
    webElem <- remDr$findElement('css selector', "body")
    remDr$executeScript("scrollTo(0, document.body.scrollHeight)", args=list(webElem))
    ```

  * 다른 태그의 스크롤

    ```R
     remDr$executeScript("var dom=document.querySelectorAll('css 선택자')[arguments[0]]; dom.scrollIntoView();", list(index))
    ```

    

---



## 예시 코드

#### 네이버 호텔 모든 댓글 추출

```R
remDr <- remoteDriver(remoteServerAddr = "localhost" , port = 4445, browserName = "chrome")
remDr$open()
url<-'https://hotel.naver.com/hotels/item?hotelId=hotel:Shilla_Stay_Yeoksam&destination_kor=%EC%8B%A0%EB%9D%BC%EC%8A%A4%ED%85%8C%EC%9D%B4%20%EC%97%AD%EC%82%BC&rooms=2'
remDr$navigate(url)
Sys.sleep(3)
pageLink <- NULL
reple <- NULL
curr_PageOldNum <- 0
repeat{
  # 댓글 리스트
  doms <- remDr$findElements(using = "css selector", "div.review_desc > p")
  Sys.sleep(1)
  reple_v <- sapply(doms, function (x) {x$getElementText()})
  print(reple_v)
  reple <- append(reple, unlist(reple_v))
  cat(length(reple), "\n")
  
  # 다음 버튼 클릭
  pageLink <- remDr$findElements(using='css',"div.hotel_used_review.ng-isolate-scope > div.review_ta.ng-scope > div.paginate > a.direction.next")
  remDr$executeScript("arguments[0].click();",pageLink)
  Sys.sleep(2)
    
  # 다음 버튼 비활성화 체크 방법1
  isPageEnd <- pageLink <- remDr$findElements(using='css',"div.hotel_used_review.ng-isolate-scope > div.review_ta.ng-scope > div.paginate > a.direction.next.disabled")
  if(length(isPageEnd)!=0){
    cat("종료\n")
    break
  }
    
  # 다음 버튼 비활성화 체크 방법2
  if(pageLink$getElementAttribute("class") == "direction next disabled"){
    cat("종료\n")
    break
  }
}
cat(length(reple), "개의 댓글 추출\n")
write(reple,"output/hotel.txt")
```



#### 브라우저 화면 스크린샷

```R
install.packages("base64enc")
install.packages("magick")
library(base64enc)
library(magick)

remDr <- remoteDriver(remoteServerAddr = "localhost", port=4445, browserName="chrome")
remDr$open()
remDr$navigate("https://google.com")


# this returns a list of base64 characters
screenshot <- remDr$screenshot(display = FALSE)
# converts the base64 characters into a vector
screenshot <- base64decode(toString(screenshot), output = NULL)
# reads the vector as stores it as a PNG
screenshot <- image_read(screenshot)
image_browse(screenshot)


remDr$screenshot(display = FALSE, file="output/google.png")
pngdata <- image_read("output/google.png")
image_browse(pngdata)
```

