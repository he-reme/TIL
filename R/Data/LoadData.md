# 데이터 읽어들이기

#### 목차

* 현재 위치 출력
* 파일 열기
* 파일 찾아서 열기
* 파일 데이터 접근
* 행단위 출력
* 조건식 정보 출력
* NA 값 확인

#### csv 파일

* 구분자로 `,`를 사용하는 파일 

#### 일정한 구분자로 구성된 파일

* 구분자로 `공백`, `탭`을 사용하는 파일

#### 기타 파일

* 확장자가 `.txt` 등인 파일

#### + 문자

* 코드셋 
  * 컴퓨터에서 문자를 표현하기 위해 문자마다 부여한 숫자값
  * 각 나라마다 그 나라 고유의 코드셋이 있음
  * 한국의 os 고유 코드셋 : EUC-KR(표준) = KSC5601(한국에서) = ANSI(메모장) = CP949
  * 1990년대부터 전세계의 모든 문자들의 코드갓을 단일화시키자는 노력이 시작됨
    * UNICODE : `UTF-8`
    * 영문 1바이트, 한글 3바이트

---



### 현재 위치 출력

`getwd()`



---

​	

### 파일 열기

#### csv 파일

```R
df <- read.csv("패스")
```

* 첫 번째 줄을 컬럼명으로 자동 지정함
* `read.csv("상대패스")`
  * 상대패스 : `data/score.csv`
* `read.csv("절대패스")`
  * 절대패스 : `c:/KHR/Rexam/data/score.csv`

#### 엑셀 파일

```R
install.packages("xlsx")
library(xlsx)
df <- read.xlsx("패스", sheetIndex, encoding="UTF-8")
```

* `sheetIndex` : 엑셀의 시트 번호

#### 일정한 구분자로 구성된 파일

> 열 갯수가 같아야 함

```R
df <- read.table("패스" [, 옵션])
```

* 첫 번째 줄을 컬럼명으로 자동 지정하지 않음
  * 임의로 지정해줌
  * 첫 번째 줄을 컬럼명으로 지정 : `df <- read.table("패스", head=T)`
* `stringAsFactors=T` : 문자열은 펙터형으로 읽음
* `header`
  * `header=T` : 첫번째 행을 열이름으로 읽고싶을 때
  * `header=F`  : 기본값
* `read.table("상대패스")`
  * 상대패스 : `data/score.log`
* `read.csv("절대패스")`
  * 절대패스 : `c:/KHR/Rexam/data/score.log`

#### 기타 파일

> 열 갯수가 다를 수 있음
>
> 수치 데이터

* **수치 데이터(숫자) 읽는 데** 특화된 파일 읽기 방법

  ```R
  nums <- scan("패스")
  ```

  * 하나라도 숫자가 아닌 값이 있을 시 에러
  * 주로 벡터로 리턴

* **character 벡터**로 읽기 방법

  ```R
  words_ansi <- scan("패스", what="")
  words_utf8 <- scan("패스", what="", encoding="코드셋")
  ```

  * `encoding="코드셋"`을 생략하고 읽으면 os의 고유 코드셋 정보를 반영해서 읽음
    * 한국의 os 고유 코드셋 : EUC-KR(표준) = KSC5601(한국에서) = ANSI(메모장) = CP949
  * 그래서 `UTF-8`로 작성된 파일을 읽으면, 한글이 깨질 수 있으므로 지정해줘야 함.
    * `encoding="UTF-8"`

* **한 행씩** 읽기

  ```R
  lines_ansi <- readLines("패스")
  lines_utf8 <- readLines("패스", encoding="UTF-8")
  ```



---



### csv 파일 찾아서 열기

```R
df <- read.csv(file.choose())
```



---



### csv 파일 데이터 접근

* `df$컬럼이름`
* `df[,c(컬럼이름 ,컬럼이름, 컬럼이름)]`
* `subset(df, select = c(컬럼이름, 컬럼이름, 컬럼이름))`
* 그냥 데이터프레임과 동일



---



### csv 파일 쓰기

```R
write.csv("")
```



### 일정한 구분자로 구성된 파일 쓰기

```R
write.table("")
```



### 기타 파일 쓰기

```R
write(memo, file="memo_new.txt")
```



---



### 행단위 출력

* `head(df)`
  * 기본값 : 1 ~ 6 행 출력
* `head(df, n=1)`
  * 1행만 출력



---



### 조건식 정보 출력 ★★★★

> `df(조건, c("컬럼명", "컬럼명", ...)`
>
> `subset(df, subset=(조건), select=c("컬럼명", "컬럼명", ...))`
>
> `subset(df, 조건, c("컬럼명", "컬럼명", ...))`

(1) name이 HyeRim인 행만 출력

* `df[df$name=="HyeRim", ]`
* `subset(df, subset=df$name=="HyeRim")`
* `subset(df, df$ename="HyeRim")`

(2) 커미션이 정해지지 않은(NA) 직원들의 모든 정보 출력

* `emp[is.na(emp$comm),]`

(3) 커미션을 받는 직원들의 모든 정보 출력

* `emp[is.na(emp$comm),]`
* `subset(emp, !is.na(emp$comm))`

(4) `select ename,sal from emp where sal>=2000`

* `emp[emp$sal>=2000,c("ename","sal")]`

* `subset(emp, emp$sal>= 2000, c("ename","sal"))`
* `subset(emp, select=c("ename","sal"), subset= emp$sal>= 2000)`

(5) `select ename,sal from emp where sal between 2000 and 3000`

* `emp[emp$sal>=2000 & emp$sal <=3000, c("ename","sal")]`
* `subset(emp, sal>=2000 & sal<=3000, c("ename","sal"))`

(6) 직무가 ANALYST가 아닌 사원들의 이름, 월급, 부서번호 출력

* `subset(emp, job!="ANALYST", c("ename", "sal", "deptno"))`

(7) 직무가 SALESMAN 이거나 ANALYST인 사원들의 이름, 직업 출력

* `subset(emp, job=="SALESMAN" | job=="ANALYST", c("ename", "job"))`



---



### NA 값 확인

`is.na(df$컬럼이름)`

* `NA` 이면 `TRUE`
* 아니면 `FALSE`



---



### 특정 열을 기준으로 오름차순 출력

`df[order(df$컬럼이름),]`



---



### 특정열의 값 마다 갯수 출력

* 부서별 직원이 몇 명인지 출력

  ```R
  info <- factor(emp$depno)
  summary(info)
  ```

* 직무별 직원이 몇 명인지 출력

  ```R
  info <- factor(emp$job)
  summary(info)
  ```

  

---


