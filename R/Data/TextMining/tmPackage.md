# tm 패키지

> text mining 패키지

* 텍스트는 기본적으로 비정형 데이터로서, 분석에 방해가 되는 요소들이 포함되어 있어서 데이터 정제 작업 필수
* tm 패키지는 텍스트 데이터의 정제 작업을 지원하는 다양한 변환 함수를 제공



---



## 주요 함수

#### `getTransformation()`

* 이 함수를 수행시키면 사용 가능한 변환 함수의 리스트 확인 가능
* 함수 리스트
  * `removeNumbers`
  * `removePunctuation`
  * `removeWords`
  * `stemDocument`
  * `stripWhitespace`

#### `tm_map()`

* `getTranformation()` 함수를 통해 확인한 함수들을 

* `tm_map()` 함수에 인수로 전달하여 변환 작업 처리 가능

* 문서에서 문장 부호를 제거하거나, 문자를 모두 소문자로 바꾸거나, 단어의 어간을 추출해주는 스테밍(stemming) 적용 가능

* **코퍼스**

  * corpus, 말뭉치
  * **tm 패키지에서 문서를 관리하는 기본 구조, 텍스트 문서들의 집합**

* 정의

  ```R
  tm_map{
  	x, # 코퍼스 객체
  	FUN # 변환에 사용할 함수
  }
  ```

#### 사용

* 여러 개의 공백을 하나의 공백으로 변환

  ```R
  corp <- tm_map(myCorpus, stripWhitespace)
  ```

* 숫자 제거

  ```R
  corp <- tm_map(myCorpus, removeNumbers)
  ```

* 영문 대문자를 소문자로 변환

  ```R
  corp <- tm_map(myCorpus, content_transformer(tolower))
  ```

* 마침표, 콤마, 세미콜론, 콜론 등 문자 제거

  ```R
  corp <- tm_map(myCorpus, removePunctuation)
  ```

* 불용어 제거 (전치사, 관사 등)기본 불용어 외에 불용어로 쓸 단어 추가

  ```R
  stopwords <- c(stopwords('en'), "and", "but") # 기본 불용어 외에 불용어로 쓸 단어 추가
  corp <- tm_map(corp, removeWords, stopwords) # 제거
  stopwords() # 불용어 확인
```

#### 숫자, 특수문자, 불용어 삭제하기 1

```R
mystopwords <- readLines("data/stopwords_ko.txt", encoding="UTF-8") # 불용어 리스트
text <- readLines("data/stopwords_testdata.txt", encoding="UTF-8")

docs <- VCorpus(VectorSource(text))
docs <- tm_map(docs, removeNumbers) # 숫자 제거
docs <- tm_map(docs, removePunctuation) # 특수문자 제거
docs <- tm_map(docs, removeWords, mystopwords) # 불용어 제거
tdm <- TermDocumentMatrix(docs, control=list(wordLengths = c(1, Inf)))
as.matrix(tdm)
```

#### 숫자, 특수문자, 불용어 삭제하기 2

```R
mystopwords <- readLines("data/stopwords_ko.txt", encoding="UTF-8") # 불용어 리스트
text <- readLines("data/stopwords_testdata.txt", encoding="UTF-8")

docs <- Corpus(VectorSource(text))
tdm <- TermDocumentMatrix(docs, control=list(
  removePunctuation = T,  # 특수문자 제거
  removeNumbers = T, # 숫자 제거
  wordLengths = c(1, Inf),
  stopwords=mystopwords)) # 불용어 제거
as.matrix(tdm)


stopwords()
```







---



## 코퍼스

* corpus, 말뭉치
* **tm 패키지에서 문서를 관리하는 기본 구조, 텍스트 문서들의 집합**

* 언어학에서 구조를 이루고 있는 텍스트 집합
* 통계 분석 및 가설 검증, 언어 규칙의 검사 등에 사용됨
* 텍스트 마이닝을 위해 수행해야 할 첫 번째 작업
  * 비정형 텍스트를 구조화된 데이터로 변환하는 것
  * 텍스트를 구조화하는 방법 중 **코퍼스(단어 주머니) 접근법**이 일반적으로 많이 사용됨

#### 코퍼스 접근법

* 분석 대상이 되는 개별 텍스트(문서)를 단어의 집합으로 단순화시킨 표현 방법
* 단어의 순서나 문법은 무시하고, **단어의 출현 빈도만을 이용**하여 텍스트를 **매트릭스로 표현**
* **매트릭스**는
  * TDM (term-document-matrix),
  * 혹은 DTM (document-term-matrix) 라고 불림

#### 코퍼스 형식으로 변환

* 분석해야 할 텍스트를 문서들의 집합인 코퍼스 형식으로 변환해야 함
* tm 패키지의 `Corpus()` 함수 사용
  * 이 함수는 다양한 소스로부터 읽어들인 텍스트를 텍스트 마이닝을 위한 Corpus 객체로 변환함
  * `VCorpus()` : 한국어 잘 출력됨
  * `Corpus()` : 영어 쓸 땐 이거 써도 무방
* `getSources()` 함수를 사용하면 사용 가능한 소스 객체 종류 파악 가능
  * 소스 객체 종류
    * `DataframeSource`
    * `DirSource`
    * `URISource`
    * `VectorSource` 
    * `XMLSource`
    * `ZipSource`



---



## 사용하기

> VectorSource

#### 패키지 설치

```R
install.packages("tm")
library(tm)
```

#### TDM 생성하기

```R
lunch <- c("커피 파스타 치킨 샐러드 아이스크림",
           "커피 우동 소고기김밥 귤",
           "참치김밥 커피 오뎅",
           "샐러드 피자 파스타 콜라",
           "티라무슈 햄버거 콜라",
           "파스타 샐러드 커피"
) # 벡터

cps <- VCorpus(VectorSource(lunch)) # 벡터 소스를 코퍼스 형식으로 변환
tdm <- TermDocumentMatrix(cps) # 문서 만들기 (TDM으로 변환)
tdm # 속성 보여줌
m <- as.matrix(tdm) # 데이터를 Matrix 형태로 보려면 형변환 해줘야 함
```

* `as.matrix(tdm)`결과

  ```R
              Docs
  Terms       1 2 3 4 5 6
    샐러드     1 0 0 1 0 1
    소고기김밥  0 1 0 0 0 0
    아이스크림  1 0 0 0 0 0
    참치김밥   0 0 1 0 0 0
    티라무슈   0 0 0 0 1 0
    파스타     1 0 0 1 0 1
    햄버거     0 0 0 0 1 0
  ```

  * `terms`는 단어, `docs`는 벡터 요소

* `terms`

  * 기본적으로 `terms`는 3자 이상인 단어만 추출
  * n자 이상인 단어 추출
    * `tdm<-TermDocumentMatrix(cps, control=list(wordLengths=c(1,Inf))`
    * `Inf` : 무한대

#### 여러가지 함수

* `inspect(tdm 또는 cps)`
  * 정보 출력
* `rowSums(m)`
  * `v <- sort(rowSums(m), decreasing=T)` 로 많이 사용됨
* `colSums(m)`
* `t(m)` 
  * 행렬의 전치
* `com <- m %*% t(m) ` 
  * 동시출현 구하기 (행렬곱)
  * 한 문장, 문단 또는 텍스트 단위에서 같이 출현한 단어를 가리킴



---



## 단어 가중치

> 문서에서 어떤 단어의 중요도를 평가하기 위해 사용되는 통계적인 수치

* 특정 문서 내에서 단어 빈도가 높을수록, 
* 전체 문서들에서는 그 단어를 포함한 문서가 적을수록,
* TFIDF 값이 높아지게 됨
* 즉, 문서 내에서 해당 단어의 중요도는 커지게 됨

* 예시
  * 예를들어, `혜림` 이라는 단어가 문서1, 2, 3, 4 모두에 있을 경우 모든 문서 1, 2, 3, 4 내에서 중요도는 0이 됨



#### 종류

* `TF` 
  * Term Frequency
  * 단어 빈도
* `IDF`
  * Inverse Document Frequency
  * 역문서 빈도
* `DF`
  * Document Frequency
  * 문서 빈도
* `TFIDF`
  * `TF` X `IDF`

```
m1 <- as.matrix(weightTf(tdm))
m2 <- as.matrix(weightTfIdf(tdm))
```





---



## 문서간 유사도 분석

> 문서들간에 동일한 단어 또는 비슷한 단어가 얼마나 공통으로 많이 사용 되었냐에 따라서 문서간 유사도 분석을 할 수 있음

1. 문서의 각 단어들을 수치화 하여 표현한다 -` DTM`
2. 문서간 단어들의 차이를 계산한다 - `코사인 유사도` 또는 `유클리드 거리`

```
install.packages("proxy")
library(proxy)
```

```R
dd <- NULL
d1 <- c("aaa bbb ccc")
d2 <- c("aaa bbb ddd")
d3 <- c("aaa bbb ccc")
d4 <- c("xxx yyy zzz")
dd <- c(d1, d2, d3, d4)

cps <- Corpus(VectorSource(dd))
dtm <- DocumentTermMatrix(cps) # 문서 만들기
as.matrix(dtm)
inspect(dtm)

m <- as.matrix(dtm)
com <- m %*% t(m) # 행렬곱 연산
com

dist(com, method = "cosine") # 코사인 거리
dist(com, method = "Euclidean") # 유클리드 거리
```

#### 코사인 거리

* 두 벡터 간의 코사인 각도를 이용하여 유사도를 측정

* 값 (0-1)
  * `0` : 완전히 똑같다
  * `1` : 완전히 다르다

#### 유클리드 거리

* 두 점 사이의 유클리드 거리 공식은 피타고라스의 정리를 통해 두 점 사이의 거리를 구하는 것과 동일

* 값 (0-)
  * `0` : 완전히 똑같다

---



## 예제

* 기본

```R
lunch <- c("커피 파스타 치킨 샐러드 아이스크림",
           "커피 우동 소고기김밥 귤",
           "참치김밥 커피 오뎅",
           "샐러드 피자 파스타 콜라",
           "티라무슈 햄버거 콜라",
           "파스타 샐러드 커피"
) # 벡터

cps <- VCorpus(VectorSource(lunch)) # 벡터 소스를 코퍼스 형식으로 변환
tdm <- TermDocumentMatrix(cps) # 문서 만들기 (TDM으로 변환)
tdm # 속성 보여줌
m <- as.matrix(tdm) # 데이터를 Matrix 형태로 보려면 형변환 해줘야 함
```

* html 텍스트 마이닝 준비

```
html_parsed <- htmlParse("아무.html")
text <- xpathSApplyhtml(html.parsed, path="p", xmlValue)
text <- text[4:30]
text

docs <- VCorpus(VectorSource(text))
docs
```

