# 데이터 읽어들이기

#### 목차

* 현재 위치 출력
* csv 파일 열기
* csv 파일 찾아서 열기
* csv 파일 데이터 접근
* 행단위 출력
* 조건식 정보 출력
* NA 값 확인



---



### 현재 위치 출력

`getwd()`



---



### csv 파일 열기

```
df <- read.csv("패스")
```

* `read.csv("상대패스")`
  * 상대패스 : `data/score.csv`

* `read.csv("절대패스")`
  * 절대패스 : `c:/kjh/Rexam/data/score.csv`



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



### 조건식 정보 출력

> `subset(df, select=컬럼명들, subset=(조건))`
>
> `subset(df, 조건, 컬럼명들)`

(1) `name`이 `HyeRim`인 행만 출력

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



---



### NA 값 확인

`is.na(df$컬럼이름)`

* `NA` 이면 `TRUE`
* 아니면 `FALSE`



---

