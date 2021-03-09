# 워드 클라우드

> 키워드 빈도수에 따라 그림 그리는 것
>

* 키워드
* 빈도수

#### 워드 클라우드 패키지

```R
install.packages("wordcloud") 
install.packages("wordcloud2") # 뉴버전
library(wordcloud) # 로드
library(wordcloud2) # 로드
```



---



## 사용

#### 데이터 타입

키워드와 빈도수로 이루어진 `data.frame`

#### 저장 방법

* 방법1

  ```R
  library(htmlwidgets)
  result <- wordcloud2(data = df)
  saveWidget(result,"output/test.html",selfcontained = F)
  ```

* 방법2

  ```R
  result <- wordcloud2(data = df)
  htmltools::save_html(result,"output/test.html")
  ```

#### 브라우저에서 확인하기

`file:///C:/경로/파일명.html`

`file:///C:/KHR/Rexam/output/tmpwc3.html`



---



## wordcloud

```R
wordcloud(df$keyword, df$freq)
```

```R
windowsFonts(폰트변수명=windowsFont("폰트명")) # 폰트
wordcloud(df$keyword, df$freq,family="폰트변수명") # 폰트 설정
```

```R
windowsFonts(폰트변수명=windowsFont("폰트명")) # 폰트
wordcloud(df$keyword, df$freq, 
          min.freq = 2, # 최소 빈도수
          random.order = F,  # 랜덤으로 위치 시킬것인지
          rot.per = 0.5,  # 회전할 단어 최대 비율
          scale = c(4, 1),  # 단어 크기 범위
          colors = rainbow(20), # 색상 (무지개색으로 20가지)
          family="lett") # 폰트
```



---



## wordcloud2

* 폰트 설정

```R
wordcloud2(df, fontFamily = "폰트명")
```

* 회전할 단어 최대 비율 (0~1)

```R
wordcloud2(df, rotateRatio = 1)
```

*  단어 크기, 단어 색상 어두운색 랜덤

```R
wordcloud2(df, size=0.5, col="random-dark")
```

* 단어 크기, 단어 색상 어두운색 랜덤, 배경색

```R
wordcloud2(df, size=0.7, col="random-light", backgroundColor = "black")
```

* 클라우드 모양

```R
wordcloud2(data = df) # 기본
wordcloud2(data = df, shape = 'diamond')
wordcloud2(data = df, shape = 'star')
wordcloud2(data = df, shape = 'cardioid')
wordcloud2(data = df, shape = 'triangle-forward')
wordcloud2(data = df, shape = 'triangle')
```



---



## 예제

```
library(KoNLP)
library(wordcloud2)
useSejongDic()

text <- readLines("data/yes24.txt", encoding = "UTF-8")

# 데이터 전처리
text <- gsub("[A-Z]|[a-z]|[[:punct:]]|[[:digit:]]", "", text)

# 명사만 추출
words <- extractNoun(text)
words

# 단어의 길이가 2자 이상이고 4자 이하인 단어만 필터링
undata <- unlist(words)
undata <- Filter(function(x) {nchar(x) >= 2 & nchar(x) <= 4}, undata)

# 단어의 개수를 셈
word_table <- table(undata)
word_table

# 많은 순으로 정렬
final <- sort(word_table, decreasing = T)

# 데이터 프레임으로 만듬
df <- data.frame(final)
names(df) <- c("keyword", "freq")

# 워드 클라우드
result <- wordcloud2(data=df, fontFamily = "휴먼옛체")

# 저장
htmltools::save_html(result,"output/yes24.html")
```

