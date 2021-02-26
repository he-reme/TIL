# R

> 통계 계산과 그래픽을 위한 프로그래밍 언어/소프트웨어 환경/프리웨어

* 인터프리터 언어
* 모듈X, 패키지O

#### 환경

* R 4.0.4
* RStudio 1.4.1103

#### 목차

* RStudio
* 기본
* 자료형
* 리터럴
* 데이터셋
* 연산자
* 제어문
* 함수
* 파일에 있는 데이터 읽기
* 객체 저장 및 로드
* 예시



---



## RStudio

#### File 탭

* 현재 인식되고 있는 폴더 위치의 파일 목록

#### Plots 탭

* 기본 그래프 출력

#### Packages 탭

* R 4.0.4 설치 시 설치된 패키지 목록
* 체크박스
  * 체크O: 기본으로 로드 되는 패키지
  * 체크X: 로드하고 사용해야 하는 패키지

#### Viewer 탭

* 웹 기반 차트, 동적 그래프 출력
* like 단순한 웹 브라우저

#### environment 탭

* 변수 값 확인



---



## 기본

* 변수에 값 대입

  ```R
  v = 100
  v <- 100
  ```

* 출력

  ```R
  print(v)
  (v<-letters[1:10]) # 연산과 동시에 출력 ()
  ```

* 지금까지 만들어진 변수 리스트 출력

  ```R
  ls()
  ```

* 변수 삭제

  ```R
  rm(변수명)
  ```

* **논리식**에 맞는 요소의 **인덱스**를 출력  (`order`처럼) ★★★

  * `which` 

  ```
  x <- (10, 2, 7, 4, 15)
  which(x>5) # 1 3 5
  ```

  ```R
  which.max(x) # x에서 max 요소를 찾고, 해당 인덱스 반환
  which.min(x) # x에서 min 요소를 찾고, 해당 인덱스 반환
  ```

* 랜덤 추출

  * `sample()`

  ```R
  sample(1:20, 3) # 1~20중 3개 랜덤으로 추출
  sample(1:10, 7, replace=T) # 중복 값 허용
  ```

* 문자열 합치기 ★★★

  * `paste()`

  ```R
  fruit <- c("Apple", "Banana", "Strawberry")
  food <- c("Pie", "Juice", "Cake")
  ```

  ```R
  paste(fruit) # "Apple Banana Strawberry"
  paste(fruit, sep="") # "AppleBananaStrawberry"
  paste0(fruit) # "AppleBananaStrawberry" . sep="" 준 것과 동일
  ```

  ```R
  paste(fruit, food. sep="") # "ApplePie" "BananaJuice" "StrawberryCake"
  paste(fruit, food, sep="-") # "Apple-Pie" "Banana-Juice" "Strawberry-Cake"
  paste(fruit, food, sep="", collapse="-") # "ApplePie-BananaJuice-StrawberryCake"
  paste(fruit, food, sep="", collapse="") # "ApplePieBananaJuiceStrawberryCake"
  paste(fruit, food, collapse=", ") # "Apple Pie, Banana Juice, Strawberry Cake"
  ```

* 내장 데이터셋

  * 목록 확인하기 : `data()`



---



## 자료형

* **문자형(character)** : 문자, 문자열
* **수치형(numeric)** : 정수, 실수
* **복소수형(complex)** : 실수+허수
* **논리형(logical)** : 참값과 거짓값



## 리터럴

* **문자열 리터럴** : "가나다", '가나다', "", ", '123', "abc"
* **수치형 리터럴** : 100, 3.14, 0
* **논리형 리터럴** : `TRUE(T)`, `FALSE(F)`
* **NULL** : 데이터 셋이 비어있음을 의미 
* **NA **: 데이터 셋의 내부에 존재하지 않는 값(결측치)를 의미 (데이터 셋은 있는데 값이 비어있을 때)
* **NaN **: not a number, 숫자가 아님
* **Inf** : 무한대 값



#### 타입 체크 함수

* `is.character(x)` : 문자형
* `is.logical(x)` : 논리형
* `is.numeric(x)` : 수치형
* `is.double(x)` : 실수형
* `is.integer(x)` : 정수형
* `is.null(x)`
* `is.na(x)`
* `is.nan(x)`
* `is.finite(x)`
* `is.infinite(x)`

#### 자동형변환 룰

* 벡터와 같이 동일한 데이터만을 가지는 데이터셋에 다른 데이터 타입이 있는 경우
* 우선순위에 맞춰 나머지도 자동으로 형변환됨

* 문자열 > 복소수형 > 수치형 > 논리형

#### 강제형변환 함수

* `as.character(x)`
* `as.integer(x)`
* `as.complex(x)`
* `as.logical(x)`
* `as.numeric(x)`
* `as.double(x)`
* `as.factor(x)`

#### 자료형 또는 구조 확인 함수

* `class(x)`
* `str(x)`
* `mode(x)`
* `typeof(x)`



---



## 데이터셋

* 벡터
* 행렬(매트릭스)
* 배열
* 데이터프레임
* 리스트

#### 구분

* 모든 유형의 객체 집합 : 리스트
* 동일한 유형의 데이터 : 배열 > 행렬 > 요인, 벡터 > 스칼라
* 서로 다른 유형의 데이터 :  데이터프레임



##### ... 자세한 내용은 DataSet 폴더에



---



## 연산자

* `$` : 성분 추출
* `^` `**` : 제곱 연산자
* `-` : 음의 부호 연산자
* `:` : 연속된 데이터 정의
* `%*%` : 행렬의 곱
* `%/%` : 몫 연산자
* `%%` : 나머지 연산자
* `+` `-` `*` `/`
* `<` `>` `<=` `>=` `==` `!=`
* `!` : 부정 연산자
* `&` `&&` `|` `||`
* `<<-` : 전역 할당 연산자
* `<-` `=` `->` : 할당 연산자
  * `<-` 사용 권장



---



## 제어문

> ControlStatement.md 참고

* for
* while
* reqeat
* if
* else if
* else
* break
* next



---



## 함수

> 자세한 함수 정의와 사용법은 Function.md 확인

### 내장함수

* `sort(v)`

  * 시퀀스형 값 오름차순으로 정렬하기

* `order(v)`

  * 시퀀스형 값 오름차순 정렬에 대한 인덱스

  

---



## 파일에 있는 데이터 읽기

* csv
* xml
* json
* 엑셀
* txt



---



## R의 데이터 입출력

> day3 보면서 다시 정리......

* `print(출력데이터 [, 옵션들])`
  * 옵션
    * `quote = FALSE` : `" "` 없애고 출력
    * `print.gap=10`
  * 데이터 구조 그대로 출력
* `cat(출력데이터 [, 옵션들])`
  * 옵션
    * `"\n"`
    * `sep="-"`

* `"R", "은 통계분석", "전용 언어입니다."` 이어서 출력하기

  * `print(paste("R", "은 통계분석", "전용 언어입니다."))`
  * `cat("R", "은 통계분석", "전용 언어입니다.")`

  

---



### 객체 저장 및 로드

```R
save()
load()
```

* 객체를 저장하고 로드할 수 있다.

* 확장자는 `.rda` 혹은 `.RData` 권장

* 특정 데이터셋 저장

  ```R
  str(v)
  str(df)
  # 확장자는 .rda 혹은 .RData 권장
  save(list=c("v", "df"), file="one.rda")
  rm(v, df)
  load("one.rda")
  ```

  * 저장된 `one.rda` 파일은 현재 폴더에 저장되어 있는 것을 확인할 수 있음
  * 이는 `load(one.rda)`로 불러올 수 있음

* 모든 데이터셋 저장

  ```R
  ls()
  length(ls())
  save(list=ls(),file="all.rda")
  rm(list=ls()) # 모든 객체 삭제
  ls()
  load("all.rda")
  ls()
  ```

  





---



## 예시

* 강수량 예시

  ```R
  rainfall <- c(21.6, 23.6, 45.8, 77.0, 
                102.2, 133.3,327.9, 348.0, 
                137.6, 49.3, 53.0, 24.9)
  rainfall > 100
  rainfall[rainfall > 100]
  which(rainfall > 100)
  month.name[which(rainfall > 100)]
  month.abb[which(rainfall > 100)]
  month.korname <- c("1월","2월","3월",
                     "4월","5월","6월",
                     "7월","8월","9월",
                     "10월","11월","12월")
  month.korname[which(rainfall > 100)]
  which.max(rainfall)
  which.min(rainfall)
  month.korname[which.max(rainfall)]
  month.korname[which.min(rainfall)]
  ```

  
