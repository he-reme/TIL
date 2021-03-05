# 정적 스크래핑





---



### 데이터 수집

* 데이터 수집을 위해서는 웹 스크래핑, 웹 크롤링 2가지 기술 필요
* 웹 스크래핑 (web scraping)
  
  * 웹 사이트 상에서 원하는 부분에 위치한 정보를 컴퓨터로 하여금 자동으로 추출하여 수집하는 기술
* 웹 크롤링 (web crawling)
  
* 자동화 봇인 웹 크롤러가 정해진 규칙에 따라 복수 개의 웹 페이지를 브라우징 하는 행위
  
* CSS 선택자에 대해 정리 잘 되어있는 블로그

  [너무 잘 정리되어있는 블로그.. 감사합니당](https://webzz.tistory.com/357)

---



### 스크래핑하려는 페이지에서 원하는 태그 찾기

#### 방법1 : CSS Selector

* CSS Selector 가져오기

  * 크롬의 개발자도구 - 원하는 부분 마우스 우클릭 - copy - copy selector

* 사용 방법 (풀버전, 간단하게 만드는 방법)

  ```R
  #1 풀버전
  "body > div > div > div.container.ng-scope > div.content > div.hotel_used_review.ng-isolate-scope > div.review_ta.ng-scope > ul > li:nth-child(2) > div.review_desc > p"
  
  #2 앞에 생략하기
  "div.review_desc > p"
  
  #3 자손 설정으로 더 정확하게 생략하기
  "div.review_ta.ng-scope div.review_desc > p"
  ```

#### 방법2 : XPath

* XPath(XML Path Language)

  * W3C의 표준으로 확장 생성 언어 문서의 구조를 통해 경로 위에 지정한 구문을 사용하여 항목을 배치하고 처리하는 방법을 기술하는 언어

* **xPath 가져오기**

  * 크롬의 개발자도구 - 원하는 부분 마우스 우클릭 - copy - copy xpath 하면 끝~!
  * 가끔 원하는 결과가 나오지 않을 때는 앞부분 지우고 `//`로 생략해보기

* 속성명 사용 방법 : `@속성명`

* 예시

  ```html
  <wikimedia>
      <projects>
      	<project name="Wikipedia" launch="2001-01-05">
              <editions>
              	<edition language="English">en.wikipedia.org</edition>
              	<edition language="German">de.wikipedia.org</edition>
                  <edition language="French">fr.wikipedia.org</edition>
                  <edition languag="Polish">pl.wikipedia.org</edition>
              </editions>
          </project>
          <project name="Wiktionary" launch="2002-12-12">
          	<editions>
                  <edition language="English">en.wiktionary.org</edition>
                  <edition language="French">fr.wiktionary.org</edition>
                  <edition language="Vietnamese">vi.wiktionary.org</edition>
                  <edition language="Turkish">tr.wiktionary.org</edition>
              </editions>
          </project>
      </projects>
  </wikimedia>
  ```

  * 모든 `project` 요소의 `name` 속성을 선택
    * `/wikimedia/projects/project/@name`
  * 모든 영문 `Wikimedia` 프로젝트의 주소 (`language` 속성이 `English`인 모든 `edition` 요소의 `문자열`)을 선택
    * `/wikimedia/projcts/project/editions/edition[@language="English"]/text()`
    * `//editions/edition[@language="English"]/text()`
    * `/` : 최상위,  `//` : 중간
  * 모든 위키백과의 주소(`Wikipedia`의 이름 특성을 가진 `project` 요소 아래에 존재하는 모든 `edition` 요소의 `문자열`)을 선택
    * `/wikimedia/projects/project[@name="Wikipedia"]/editions/edition/text()`

---



### 정적 웹 페이지 스크래핑에 사용되는 주요 API

#### xml2 패키지

* `read_html(url)`
  * HTML 웹 페이지를 요청해서 받아오기

#### rvest 패키지

* `html_nodes(x, css, xpath)` / `html_node(x, css, xpath)`
  * 원하는 노드(태그) 추출하기
  * css 혹은 xpath 선택
    * 단, xpath일 경우 키워드 줘야 함
    * css는 생략 가능
* `html_text(x, trim=FALSE)`
  * 노드에서 컨텐츠 추출하기
  * `trim=TRUE` : 분리문자 제거
* `html_attrs(x)`
  * 노드에서 속성들 추출하기
* `html_attr(x, name, default="")`
  * 노드에서 주어진 명칭의 속성값 추출하기

#### xml 패키지

* 응답 내용이 `html`일 경우에도 사용 가능

* `htmlParse(file, encoding="...")`
  
* `xpathSApply()` 사용 가능한 객체로 변환
  
* `xpathSApply(doc, xpath, fun)`

  * 원하는 노드(태그) 추출하고 전달된 함수 수행하기
  * `fun` : `xmlValue`, `xmlGetAttr`, `xmlAttrs`

* 예시

  ```R
  imsi <- read_html("url")
  t <- htmlParse(imsi)
  content<- xpathSApply(t,'xpath', xmlValue); 
  content
  ```

#### httr 패키지

* `GET(url)`
  * HTML 웹 페이지를 요청해서 받아오기
  * `read_html(url)` 보다 좀 더 기능이 확장됨
  * **요청 헤더**에 **계정 또는 패스워드** 등의 정보 전달 가능
  * 응답 내용이 **바이너리**인 경우에도 사용 가능
    * pdf, 이미지 등



---



### rvest 패키지 사용 순서

```R
url <- "url" # 스크래핑할 url
html <- read_html(url) # 해당 url의 html 가져오기
h1 <- html_node(html, "h1") # 가져온 html에서 원하는 태그 1개 가져오기
h1s <- html_nodes(html, "h1") # 가져온 html에서 원하는 태그들 가져오기
```

```R
h1_content <- html_text(h1) # 해당 태그의 컨텐츠 가져오기
h1_attrs <- html_attrs(h1) # 해당 태그의 속성들 추출
h1_attr <- html_attr(h1, 속성명) # 해당 태그의 속성명을 통한 속성값 추출
```



### xml 패키지 사용 순서

```R
url <- "url"
html <- read_html(url)
hp <- htmlParse(html) # xpathSApply() 사용할 수 있는 객체로 변환
```

```R
h1 <- xpathSApply(hp, xpath, xmlValue) # 해당 태그의 컨텐츠 가져오기
h1 <- xpathSApply(hp, xpath, xmlGetAttr) # 확인 해야함
h1 <- xpathSApply(hp, xpath, xmlAttrs) # 확인 해야함
```



### httr 패키지 사용 순서

>  이미지, 첨부파일 다운받기 

```R
# pdf
res <- GET('url/아무거나.pdf')
writeBin(content(res, 'raw'), '저장경로/원하는이름.pdf')
```

```R
# jpg
html <- read_html('url')
imgs <- html_nodes(html, 'img')
img.src <- html_attr(imgs, 'src')
for(i in 1:length(img.src)){
	res <- GET(paste('다운받을 url', img.src[i], sep=""))
	writeBin(content(res, 'raw'), paste('저장경로', img.src[i], sep=""))
}
```

* 이해 안되면 아래에 예제



---



### 스크래핑할 태그 정보 얻기

#### chrome의 개발자 도구 활용

* 이상한 유니코드 형식일 경우 
  * 크롬에 검색하면 백과사전 나오는데 들어가서 복사 ㄱㄱ



#### DOM 객체의 구조



---



### 같이 사용하면 좋은 함수

* `unique()` : 중복 결과 제거



---



#### 예시(연습) 코드

```R
url <- "http://unico2013.dothome.co.kr/crawling/exercise_bs.html"
html <- read_html(url)

h1 <- html_node(html, "h1")
h1_content <- html_text(h1)
h1_content

# a태그의 href 속성값
a <- html_nodes(html, "a")
a_href <- html_attr(a, "href")
a_href

# img태그의 src 속성값
img <- html_node(html, "img")
img_src <- html_attr(img, "src")
img_src

h2_1 <- html_nodes(html, "h2:nth-of-type(1)")
h2_1_content <- html_text(h2_1)
h2_1_content

# ul태그의 자식 태그 중 style 속성값이 green으로 끝나는 태그의 컨텐츠
li <- html_nodes(html, "ul>li[style$='green']")
li_content <- html_text(li)
li_content

# h2태그의 2번째 자식의 컨텐츠
h2_2 <- html_nodes(html, "h2:nth-of-type(2)")
h2_2_content <- html_text(h2_2)
h2_2_content

# ol태그의 직계 자손 (모든 자식)의 컨텐츠
ol_child <- html_nodes(html, "ol>*")
ol_child_content <- html_text(ol_child)
ol_child_content

# table태그의 모든 자손의 컨텐츠
table_child <- html_nodes(html, "table *")
table_child <- html_text(table_child)
table_child

# name이라는 클래스 속성을 갖는 tr태그의 컨텐츠
tr_name <- html_nodes(html, "tr.name")
tr_name_content <- html_text(tr_name)
tr_name_content

# target이라는 아이디 속성을 갖는 td태그의 컨텐츠
td_target <- html_nodes(html, "td#target")
td_target_content <- html_text(td_target)
td_target_content
```



---



### 영화 사이트 (Naver)

#### 영화 제목, 평점, 리뷰글 읽기

```R
text<- NULL; vtitle<-NULL; vpoint<-NULL; vreview<-NULL; page=NULL
url<- "http://movie.naver.com/movie/point/af/list.nhn"
text <- read_html(url,  encoding="CP949")
text

for (index in 1:10) {
  # 영화제목
  node <- html_node(text, paste0("#old_content > table > tbody > tr:nth-child(", index, ") > td.title > a.movie.color_b"))
  title <- html_text(node)
  vtitle[index] <- title
  # 영화평점
  node <- html_node(text, paste0("#old_content > table > tbody > tr:nth-child(", index,") > td.title > div > em"))
  point <- html_text(node)
  vpoint <- c(vpoint, point)
  # 영화리뷰 
  node <- html_nodes(text, xpath=paste0('//*[@id="old_content"]/table/tbody/tr[', index,"]/td[2]/text()"))
  node <- html_text(node, trim=TRUE)
  print(node)
  review = node[4] 
  vreview <- append(vreview, review)
}
page <- data.frame(vtitle, vpoint, vreview)
View(page)
write.csv(page, "output/movie_reviews1.csv")
```



#### 여러 페이지로 읽기1

> 생략된 데이터가 있는 페이지는 수집하지 않음

```R
# 여러 페이지1
site<- "http://movie.naver.com/movie/point/af/list.nhn?page="
text <- NULL
movie.review <- NULL
for(i in 1: 100) {
  url <- paste(site, i, sep="")
  text <- read_html(url,  encoding="CP949")
  nodes <- html_nodes(text, ".movie")
  title <- html_text(nodes)
  nodes <- html_nodes(text, ".title em")
  point <- html_text(nodes)
  nodes <- html_nodes(text, xpath="//*[@id='old_content']/table/tbody/tr/td[2]/text()")
  imsi <- html_text(nodes, trim=TRUE)
  review <- imsi[nchar(imsi) > 0] 
  if(length(review) == 10) {
    page <- data.frame(title, point, review)
    movie.review <- rbind(movie.review, page)
  } else {
    cat(paste(i," 페이지에는 리뷰글이 생략된 데이터가 있어서 수집하지 않습니다.\n"))
  }
}
write.csv(movie.review, "output/movie_reviews2.csv")
```



#### 여러 페이지로 읽기2

> 페이지에 생략된 데이터가 있더라도 수집

```R
site<- "http://movie.naver.com/movie/point/af/list.nhn?page="
text <- NULL
movie.allreview <- NULL
for(i in 1: 100) {
  url <- paste(site, i, sep="")
  text <- read_html(url,  encoding="CP949")
  for (index in 1:10) {
    # 영화제목
    node <- html_node(text, paste0("#old_content > table > tbody > tr:nth-child(", index, ") > td.title > a.movie.color_b"))
    title <- html_text(node)
    vtitle[index] <- title
    # 영화평점
    node <- html_node(text, paste0("#old_content > table > tbody > tr:nth-child(", index,") > td.title > div > em"))
    point <- html_text(node)
    vpoint <- c(vpoint, point)
    # 영화리뷰 
    node <- html_nodes(text, xpath=paste0('//*[@id="old_content"]/table/tbody/tr[', index,"]/td[2]/text()"))
    node <- html_text(node, trim=TRUE)
    print(node)
    review = node[4] # 질문!!
    vreview <- append(vreview, review)
  }
  page <- data.frame(vtitle, vpoint, vreview)
  movie.review <- rbind(movie.allreview, page)
  
}
write.csv(movie.review, "output/movie_reviews3.csv")
```



#### 뉴스 읽기 (다음) 1

> for 문 사용

```R
# rvest 패키지 사용
url <- "https://news.daum.net/ranking/popular/"
html <- read_html(url)

daumnews <- NULL
for(index in 1:50){
  node <- html_node(html, xpath=paste0('//*[@id="mArticle"]/div[2]/ul[3]/li[', index, ']/div[2]/strong/a'))
  newstitle <- html_text(node)
  
  node <- html_node(html, xpath=paste0('//*[@id="mArticle"]/div[2]/ul[3]/li[', index, ']/div[2]/strong/span'))
  newspapername <- html_text(node)
  
  news <- data.frame(newstitle, newspapername)
  daumnews <- rbind(daumnews, news)
}
write.csv(daumnews, "output/daumnews.csv")


# xml 패키지 사용
url <- "https://news.daum.net/ranking/popular/"
html <- read_html(url)
hp <- htmlParse(html)

daumnews <- NULL
for(index in 1:50){
  newstitle <- xpathSApply(hp, paste0('//*[@id="mArticle"]/div[2]/ul[3]/li[', index, ']/div[2]/strong/a'), xmlValue)
  newspapername <- xpathSApply(hp, paste0('//*[@id="mArticle"]/div[2]/ul[3]/li[', index, ']/div[2]/strong/span'), xmlValue)

  news <- data.frame(newstitle, newspapername)
  daumnews <- rbind(daumnews, news)
}
write.csv(daumnews, "output/daumnews.csv")
```



#### 뉴스 읽기 (다음) 2

> 한번에 구하기

```R
# rvest 패키지 사용
url <- "https://news.daum.net/ranking/popular/"
html <- read_html(url)

daumnews <- NULL

node <- html_node(html, xpath='//*[@id="mArticle"]/div[2]/ul[3]/li/div[2]/strong/a'))
newstitle <- html_text(node)
  
node <- html_node(html, xpath=paste0('//*[@id="mArticle"]/div[2]/ul[3]/li/div[2]/strong/span'))
 newspapername <- html_text(node)
  
news <- data.frame(newstitle, newspapername)
write.csv(news, "output/daumnews.csv")


# xml 패키지 사용
url <- "https://news.daum.net/ranking/popular/"
html <- read_html(url)
hp <- htmlParse(html)

daumnews <- NULL

newstitle <- xpathSApply(hp, paste0('//*[@id="mArticle"]/div[2]/ul[3]/li/div[2]/strong/a'), xmlValue)
newspapername <- xpathSApply(hp, paste0('//*[@id="mArticle"]/div[2]/ul[3]/li/div[2]/strong/span'), xmlValue)

news <- data.frame(newstitle, newspapername)
write.csv(news, "output/daumnews.csv")
```



#### 이미지 첨부파일 다운 받기

```R
# pdf
library(httr)
res = GET('http://cran.r-project.org/web/packages/httr/httr.pdf')
writeBin(content(res, 'raw'), 'c:/Temp/httr.pdf')

# jpg
h = read_html('http://unico2013.dothome.co.kr/productlog.html')
imgs = html_nodes(h, 'img')
img.src = html_attr(imgs, 'src')
for(i in 1:length(img.src)){
  res = GET(paste('http://unico2013.dothome.co.kr/',img.src[i], sep=""))
  writeBin(content(res, 'raw'), paste('c:/Temp/', img.src[i], sep=""))
} 
```



#### 네이버 웹툰

* 제목, 설명, 별점 스크래핑하고, `csv`로 저장

```R
library(rvest)
library(XML)
library(httr)

site <- "https://comic.naver.com/genre/bestChallenge.nhn?page="

comicName <- NULL; comicSummary <- NULL; comicGrade <- NULL
for(page in 1:20){
  url <- paste(site, page, sep='')
  print(url)
  html <- read_html(url)
  
  node <- html_node(html, xpath='//td/div[2]/h6/a/text()')
  comicName <- c(comicName, html_text(node, trim=TRUE))
      
  node <- html_node(html, xpath='//td/div[2]/div[1]')
  comicSummary <- c(comicSummary, html_text(node, trim=TRUE))
  comicSummary
      
  node <- html_node(html, xpath='//td/div[2]/div[2]/strong')
  comicGrade <- c(comicGrade, html_text(node, trim=TRUE))
  comicGrade
}
navercomic <- data.frame(comicName, comicSummary, comicGrade)
write.csv(navercomic, "output/navercomic.csv")
```



