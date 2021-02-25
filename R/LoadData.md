# 데이터 읽어들이기

#### 목차

* 현재 위치 출력
* csv 파일 열기
* csv 파일 찾아서 열기
* csv 파일 데이터 접근
* 행단위 출력
* 조건식 정보 출력
* NA 값 확인

#### csv 파일

* 구분자로 `,`를 사용하는 파일 

#### 일정한 구분자로 구성된 파일

* 구분자로 `공백`, `탭`을 사용하는 파일

#### 기타 파일

* 확장자가 `.txt` 등인 파일

---



### 현재 위치 출력

`getwd()`



---



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

#### 일정한 구분자로 구성된 파일

```R
df <- read.table("패스" [, 옵션])
```

* 첫 번째 줄을 컬럼명으로 자동 지정하지 않음
  * 임의로 지정해줌
  * 첫 번째 줄을 컬럼명으로 지정 : `df <- read.table("패스", head=T)`
* `stringAsFactors=T` : 문자열은 펙터형으로 읽음

* `read.table("상대패스")`
  * 상대패스 : `data/score.log`
* `read.csv("절대패스")`
  * 절대패스 : `c:/KHR/Rexam/data/score.log`

#### 기타 파일

* **수치 데이터(숫자) 읽는 데** 특화된 파일 읽기 방법

  ```R
  nums <- scan("패스")
  ```

  * 하나라도 숫자가 아닌 값이 있을 시 에러
  * 주로 벡터로 리턴



---



### csv 파일 찾아서 열기

```
df <- read.csv(file.choose())
```



---



### csv 파일 데이터 접근

* `df$컬럼이름`
* `df[,c(컬럼이름 ,컬럼이름, 컬럼이름)]`
* `subset(df, select = c(컬럼이름, 컬럼이름, 컬럼이름))`
* 그냥 데이터프레임과 동일



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

  

