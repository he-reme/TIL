# 텍스트 마이닝

> 단어의 출현 빈도, 단어 간 관계성 등을 파악하여 유의미한 정보를 추출하는 것
>
> '자연어 처리 기술'을 기반으로 함

#### 텍스트 마이닝을 통해..

* 문서들을 자동으로 분류할 수 있고, 문서나 단어들간의 연관성을 분석할 수 있으며
* 텍스트에 담겨있는 감성(평가, 성향)을 예측할 수 있고
* 시간의 흐름에 따른 이슈들의 변환 과정을 추적할 수 있다

#### 텍스트 마이닝을 잘 하기 위해서는 

* 형태소분석기나 구문분석기와 같은 자연어처리 도구를 잘 사용할 수 있어야 하고, 
* 그 외에 다루는 언어에 대해서도 잘 알고 있어야 함

#### 환경

* 언어 R
* 한글 자연어 분석 패키지 : KoNLP (Korean Natural Language Processing)



---



## 데이터 마이닝 vs 텍스트 마이닝

#### 데이터 마이닝

* 수치데이터와 범주형 데이터를 중점적으로 다룸

#### 텍스트 마이닝

* 텍스트데이터를 중점적으로 다룸

* 데이터 마이닝의 일부이나, 프로세싱이나 처리방법에서 많이 다룸
* 많은 양의 비정형 데이터에 접근하고 활용하는 데 사용됨
* 가치나 인사이트를 찾을 수 있을 뿐 아니라 
* 비정형 데이터를 관리함으로써 실질적인 ROI(Return On Investment)를 이끌어 낼 수 있음



---



## 텍스트 마이닝 개요

1. 비정형 텍스트
2. 구조화된 데이터
3. 의미있는 정보 추출
   * 연관성 분석
   * 트렌드 분석
   * 감성 분석



---



## 자연어 처리

> 자연어 : 일상생활에서 사용하는 말, 언어
>
> 자연어 처리 : 인간이 사용하는 언어를 컴퓨터가 사용할 수 있게 처리하는 것

* 자연어 처리 기술을 바탕으로 사람들이 작성한 텍스트를 컴퓨터가 분석하여 중요한 단어나 문장들을 추출할 수 있음
* 활용 예시 (자연어 처리를 통해 알아낼 수 있는 것)
  *  매력적인 뉴스 기사의 헤드라인 작성
  * 제품에 대한 고객 반응 분석
  * 우리 브랜드에 대한 고객 생각
  * 음성인식(시리, 빅스비)나 광학문자판독을 통해서 책에서 글자를 읽어 들이거나 웹 페이지에서 사람이 작성한 글을 로봇을 이용해서 크롤링 하고 해석한 후
    * 어떤 것이 핵심어이고 어떤 것이 주제어 인가 등을 알아냄
    * 글쓴이의 감정이나 상태 등을 알아냄

#### 자연어 처리

* 형태소분석기, 구문분석기와 같은 사람이 작성한 글이나 대화를 컴퓨터를 통해 해석할 수 있게 하는 소프트웨어를 개발하거나 연구하고
* 그런 것들을 이용해서 실제로 작업하는 것

#### 형태소분석기

* 형태소를 구분하고 무엇인지 알려주는 것
* 형태소 분석으로 어절들의 품사를 파악한 후 명사, 동사, 형용사 등 의미를 지닌 품사의 단어를 추출해 각 단어가 얼마나 많이 등장했는지 확인
* 잘 알려진 형태소 분석기 종류
  * Hannanum : KAIST의 한나눔 형태소 분석기와 NLP_HUB 구문분석기
  * KKMA : 서울대의 꼬꼬마 형태소/구문분석기 v2_1
  * KOMORAN : Junsso Shin님의 코모란 v3.3.3
  * Twitter : OpenKoreanText의 오픈 소스 한국어 처리기 v2_2_0 (구 Twitter 한국어 분석기)1-1
  * Eunjeon : 온전한님의 프로젝트의 SEunjeon(S온전)
  * Arirang : 이수명님의 Arirang Morpheme Analyzer 1-2
  * RHINO : 최석재님의 RHINO v2_5.4

#### 구문분석기

* 주어, 목적어, 서술어와 같은 형태로
* 품사보다는 단위가 더 높은 논리적 레벨까지 처리해주는 것



---



## 형태소 분석기

* 형태소 분석으로 어절들의 품사를 파악한 후 
* 명사, 동사, 형용사 등 의미를 지닌 품사의 단어를 추출해 각 단어가 얼마나 많이 등장했는지 확인

#### 잘 알려진 한국어 형태소 분석기 종류

* Hannanum : KAIST의 한나눔 형태소 분석기와 NLP_HUB 구문분석기
* KKMA : 서울대의 꼬꼬마 형태소/구문분석기 v2_1
* KOMORAN : Junsso Shin님의 코모란 v3.3.3
* Twitter : OpenKoreanText의 오픈 소스 한국어 처리기 v2_2_0 (구 Twitter 한국어 분석기)1-1
* Eunjeon : 온전한님의 프로젝트의 SEunjeon(S온전)
* Arirang : 이수명님의 Arirang Morpheme Analyzer 1-2
* RHINO : 최석재님의 RHINO v2_5.4

#### 연습할 때 사용한 한국어 형태소 분석 패키지

* KoNLP 패키지



---



## KoNLP 패키지

> Korean Natural Language Processing
>
> 한글 자연어 분석 패키지

```R
install.packages("KoNLP")
library(KoNLP)
```

#### 다운로드 방법

```R
install.packages("Sejong")
install.packages("hash")
install.packages("tau")
install.packages("devtools")
# github 버전 설치
install.packages("remotes")
# 64bit 에서만 동작합니다.
remotes::install_github('haven-jeon/KoNLP', upgrade = "never", INSTALL_opts=c("--no-multiarch"))
library(KoNLP) # 임포트 확인
```

#### 문자

> 더 자세한 내용은 ''한나눔에서 사용하는 카이스트 품사 태그 셋' 에서 확인'

* `S` : 기호
* `F` : 외국어
* `N` : 체언 (명사, 대명사, 수사)
  * NC : 보통명사
  * NQ : 고유명사
  * NB : 의존명사
  * NP : 대명사
  * NN : 수사
* `P` : 용언 (동사, 형용사)
  * PV : 동사
  * PA : 형용사
  * PX : 보조용언
* `M` : 수식언 (관형사, 부사)
  * MM : 관형사
  * MA : 부사
* `I` : 독립언 (감탄사)
* `J` : 관계언 (조사)
  * JC : 격조사
* `E` : 어미
* `X` : 접사

#### SejongDic 사용하기

```R
# 명사가 제대로 뽑아지지 않는 경우. 해당 명사가 딕셔너리에 없기 때문이므로 
# 해당 명사를 추가해줘야 한다.
add_words <- c("백두산", "남산", "철갑", "가을", "달", "구름")
buildDictionary(user_dic=data.frame(add_words, rep("ncn", length(add_words))), replace_usr_dic=T)
```

#### 예제

* 예제1

````R
extractNoun("대한민국의 영토는 한반도와 그 부속도서로 한다")
# [1] "대한민국" "영토" "한반도" "부속도서" "한"
````

* 예제2 ( 요즘엔 extracNoun만 써도 같은 결과 ㅇㅇ )

```R
sapply("대한민국의 영토는 한반도와 그 부속도서로 한다", extractNoun, USE.NAMES=F)
#      [,1]
# [1,] "대한민국"
# [2,] "영토"
# [3,] "한반도"
# [4,] "부속도서"
# [5,] "한"
```

* 예제3

```R
SimplePos22("대한민국의 영토는 한반도와 그 부속도서로 한다")
SimplePos09("대한민국의 영토는 한반도와 그 부속도서로 한다")
```



---



## 예제

#### 애국가에서 가장 많이 나오는 단어 TOP10 구하기

* data.frame 형태로 만들어 csv에 저장

```R
library(KoNLP)
useSejongDic()

text <- readLines("data/애국가(가사).txt")
text

words <- extractNoun(text)
words

undata <- unlist(word_data3)
undata

words_table <- table(undata)
words_table

final <- sort(words_table, decreasing = T)
final

df <- data.frame(head(final, 10)) # top10 뽑아주기
colnames(df) <- c("word", "count") # 열 이름 설정

write.csv(df, file="output/top10.csv")
```



#### 애국가에서 단어 길이가 2 이상, 4 이하인 단어만 구하기

```R
library(KoNLP)
useSejongDic()

text <- readLines("data/애국가(가사).txt")
text

words <- extractNoun(text)
words

undata <- unlist(word_data3)
undata

undata2 <- Filter(function(x) {nchar(x) >= 2 & nchar(x) <= 4}, undata) # 길이 2 이상 4 이하

words_table <- table(undata2)
words_table
```

