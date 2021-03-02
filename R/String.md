# 문자열

#### 목차

* 날짜와 시간 관련 함수
* 문자열 대체
* 문자열 찾기
* 문자열 쪼개기
* 문자열 처리 관련 주요 함수들



---



### 날짜와 시간 관련 함수

#### 기본

* 현재 날짜

  ```R
  Sys.Date()
  ```

* 현재 날짜 및 시간

  ```R
  Sys.time()
  ```

* 미국식 날짜 및 시간

  ```R
  date()
  ```

* 타임존

  ```R
  Sys.timezone() # Asia/Seoul
  ```

* "0000-00-00" 로 출력

  ```R
  as.Date('2018/1/15') # 표준 서식이므로 format 생략 가능
  as.Date('1/15/2018',format='%m/%d/%Y')
  as.Date('4월 26, 2018',format='%B %d, %Y')
  as.Date('110228',format='%d%b%y') # NA
  as.Date('110228',format='%y%m%d')
  ```

#### 포맷

* 년월일시분초 타입의 문자열을 시간으로 변경

  ```R
  as.Date("년-월-일 시:분:초")
  as.Date("년/월/일 시:분:초")
  ```

* 문자열을 날짜형으로

  ```R
  x1 <- "2019-01-10 13:30:41"
  as.Date(x1, "%Y-%m-%d %H:%M:%S") 
  ```

* 문자열을 날짜+시간형으로

  ```R
  strptime(문자열, "포맷")
  ```

  ```R
  x1 <- "2019-01-10 13:30:41"
  strptime(x1, "%Y-%m-%d %H:%M:%S")
  strptime('2019-08-21 14:10:30', "%Y-%m-%d %H:%M:%S"
  ```

* 특정 포맷을 이용한 날짜 및 시간

  ```R
  as.Date(Date객체, format="포맷")
  format(Date객체, "포맷")
  ```

  * 예시
    * `format(Date객체, "%Y년 %m월 %d일")`
  * 포맷
    * `%d` : 일 (01~31)
    * `%a` : 요일 (축약형)
    * `%A` : 요일
    * `%m` : 월 (01~12)
    * `%b` : 월 (축약형)
    * `%B` : 월
    * `%y` : 년도 (00)

* 함수를 이용한 날짜 및 시간

  * `weekdays(Date객체)`
  * `months(Date객체)`
  * `quarters(Date객체)` : 몇 분기인지 리턴함

#### 날짜 데이터끼리 연산

* 날짜끼리 뺄셈 가능, 날짜와 정수의 덧셈뺄셈 가능

  * 하루를 1로 간주, 소숫점 생략

* 날짜 데이터끼리 연산할 때 소숫점을 표현하고자 하는 경우

  * `as.Date` 대신에 `as.POSIXct`, `as.POSIXlt` 함수 이용
  * `as.POSIXct`
  * `as.POSIXlt` : 리스트처럼 사용 가능

* 예시

  ```R
  as.Date("2020/01/01 08:00:00") - as.Date("2020/01/01 05:00:00") # 0 days
  as.POSIXct("2020/01/01 08:00:00") - as.POSIXct("2020/01/01 05:00:00") # 3 hours
  as.POSIXlt("2020/01/01 08:00:00") - as.POSIXlt("2020/01/01 05:00:00") # 3 hours
  ```

#### Date 객체 풀기

* `unclass(Date객체)`

* 1970-01-01을 기준으로 얼마나 날짜가 지났는지의 값을 가지고 있음



#### POSIXlt / POSIXct 사용

* 내가 태어난 요일 출력

  ```R
  myday<-as.POSIXlt("1997-10-17")
  weekdays(myday)
  ```

* 내가 태어난지 며칠

  ```R
  as.POSIXlt(Sys.Date()) - myday
  ```

* 올해의 크리스마스 요일

  ```R
  christmas2<-as.POSIXlt("2021-12-25")
  weekdays(christmas2) # 방법1 (요일 출력)
  christmas2$wday # 방법2 (숫자 요일 출력)
  ```

* 오늘은 xxxx년 xx월 xx일 x요일입니다 형식으로 출력

  ```R
  tmp<-Sys.Date()
  year<-format(tmp,'%Y')
  month<-format(tmp,'%m')
  day<-format(tmp,'%d')
  weekday<-format(tmp,'%A')
  paste("오늘은 ",year,"년 ",month,"월 ",day,"일 ",weekday," 입니다.",sep="")
  ```

  ```R
  tmp<-Sys.Date()
  format(tmp,'오늘은 %Y년 %B %d일 %A입니다')
  ```



---



### 문자열 대체

> sub : substitute, 대체하다

#### `gsub("찾을 문자열", "대체 문자열", "대상 문자열")`

* 여러 개 있는 경우 모두 변경
* `gsub(pattern="찾을 문자열", replace="대체 문자열", x="대상 문자열")`

#### `sub("찾을 문자열", "대체 문자열", "대상 문자열")`

* 여러 개 있는 경우 첫 번째 발견되는 하나만 변경
* `sub(pattern="찾을 문자열", replace="대체 문자열", x="대상 문자열")`

#### 정규 표현식

* `[]` 
  * or 행
* `^`
  * not

* `[A-Z]`
  * ABCDEFG...XYZ

* `[가-힣]`
  * 가갸거겨...힣
* `[0-9]`
  * 0123...89
* `[0-9][3]-[0-9][3,4]-[0-9][4]`
  * 010-1234-5678
* `*`
  * 바로 앞에 있는 문자가 0개 이상인 문자열
  * `A*B` : B, AB, AAB, AAAB, AAAAB, ... 
* `+`
  * 바로 앞에 있는 문자가 1개 이상인 문자열
  * `A+B` : AB, AAB, AAAB, AAAAB, ...

* `?`
  * 바로 앞에 있는 문자가 0개, 1개인 문자열
  * `A?B` : B, AB

#### 예시

```R
word <- "JAVA javascript 가나다 123 %^&*" # 대상 문자열
gsub("A", "", word) 
gsub("a", "", word) 
gsub("[Aa]", "", word) 
gsub("[가-힣]", "", word) 
gsub("[^가-힣]", "", word) # 가-힣 빼고 ""로 대체
gsub("[&^%*]", "", word) # &, ^, %, * 를 ""로 대체
gsub("[[:punct:]]", "", word) # 특수문자 ""로 대체
gsub("[[:alnum:]]", "", word) # 알파벳, 숫자, 한글 ""로 대체
gsub("[1234567890]", "", word) # 숫자 ""로 대체
gsub("[[:digit:]]", "", word) # 숫자 ""로 대체
gsub("[^[:alnum:]]", "", word) # 공백, 특수문자 ""로 대체
gsub("[[:space:]]", "", word) # 공백 ""로 대체
gsub("[[:space:][:punct:]]", "", word) # 공백, 특수문자 ""로 대체
gsub("[a-z]|[A-Z]", "", word) # 모든 알파벳 ""로 대체

gsub("Aa", "", word) # Aa
gsub("(Aa)", "", word)  # Aa
gsub("(Aa){2}", "", word) # AaAa
gsub("Aa{2}", "", word) # Aaa

gsub("[ABC]", "@", "123AunicoBC98ABC")
gsub("ABC", "@", "123AunicoBC98ABC")
gsub("(AB)|C", "@", "123AunicoBC98ABC")
gsub("A|(BC)", "@", "123AunicoBC98ABC")
gsub("A|B|C", "@", "123AunicoBC98ABC")
```



---



### 문자열 찾기

#### `grep()` ★★★★

```R
grep(pattern="찾을 문자열", x="대상 문자열")
grep("찾을 문자열", "대상 문자열")
grep("찾을 문자열", "대상 문자열", value=TRUE)
```

* `grep(pattern="찾을 문자열", x="대상 문자열")`

  * 찾을 문자열을 가진 문자열의 **인덱스** 반환

  * 예시

    ```R
    head(islands) # 내장 데이터셋
    landmesses <- names(islands)
    landmesses
    grep(pattern="New", x=landmesses)
    ```

* `grep("찾을 문자열", "대상 문자열", value=TRUE)`

  * 찾을 문자열을 가진 문자열 반환

  * 예시

    ```R
    grep("New", landmesses, value=T)
    # 위와 동일 코드
    index <- grep("New", landmesses)
    landmesses[index]
    ```

* 예시

  ```R
  words <- c("ct", "at", "bat", "chick", "chae", "cat", 
             "cheanomeles", "chase", "chasse", "mychasse", 
             "cheap", "check", "cheese", "hat", "mycat")
  
  grep("che", words, value=T)
  grep("at", words, value=T)
  grep("[ch]", words, value=T)
  grep("[at]", words, value=T)
  grep("ch|at", words, value=T)
  grep("ch(e|i)ck", words, value=T)
  grep("chase", words, value=T)
  grep("chas?e", words, value=T)
  grep("chas*e", words, value=T)
  grep("chas+e", words, value=T)
  grep("ch(a*|e*)se", words, value=T)
  grep("^c", words, value=T) # "ct" "chick" "chae" ... c로 시작하는 단어들
  grep("t$", words, value=T) # "ct" "at" "bat" "cat" "hat" "mycat"
  grep("^c.*t$", words, value=T) # "ct" "cat"
  ```

  

---



### 문자열 쪼개기

#### `strsplit()`

```R
strsplit(x="대상 문자열", split="구분 문자열")
strsplit("대상 문자열", "구분 문자열")
```

* 리스트로 리턴

* 예시

  ```R
  fox.said <- "What is essential is invisible to the eye"
  fox.said
  strsplit(x= fox.said, split= " ") # "What" "is" "essential" "is" "invisible" "to" "the" "eye"
  ```

  

---



### 문자열 처리 관련 주요 함수들

* `nchar()` / `length()`

  ```R
  x <- "We have a dream"
  nchar(x) # 15
  length(x) # 1
  ```

  ```R
  y <- c("We", "have", "a", "dream")
  nchar(y) # 2 4 1 5
  length(y) # 4
  ```

* `sort()`

  ```R
  sort(문자열) # 오름차순
  sort(문자열, decrasing=TRUE) # 내림차순
  ```

* `tolower()` /  `toupper()`

* `substr()` / `substring()`

  ```R
  substr("Data Analytics", start=1, stop=4) # Data
  substr("Data Analytics", 6, 14) # Analytics
  substring("Data Analytics", 6) # Analytics
  ```

  ```R
  classname <- c("Data Analytics", "Data Mining", 
                 "Data Visualization")
  substr(classname, 1, 4) # "Data" "Data" "Data"
  ```

  ```R
  # 맨 뒤 두글자 가져오기
  countries <- c("Korea, KR", "United States, US", 
                 "China, CN")
  substr(countries, nchar(countries)-1, nchar(countries)) # "KR" "US" "CN"
  ```

