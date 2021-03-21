# 데이터프레임

> data.frame

* 2차원 구조
* 열단위로 **서로 다른 타입의 데이터들로 구성 가능**
* **모든 열의 데이터 개수(행의 개수)는 동일해야 함**



---



### 생성 방법

* `data.frame(벡터들)`

  ```R
  no <- c(1,2,3,4)
  name <- c('Apple','Banana','Peach','Berry')
  qty <- c(5,2,7,9)
  price <- c(500,200,200,500)
  fruit <- data.frame(no, name, qty, price)
  ```

  * 해당 벡터들은 열 단위로 들어감

* `data.frame(열이름=벡터, ...)`

  ```R
  df <- data.frame(
    영어=c(90, 80, 60, 70), 
    수학=c(50, 60, 100, 20), 
    클래스=c(1,1,2,2)
  )
  ```

  * 열 이름 지정하며 생성

* `data.frame(벡터들...[, stringsAsFactors=FALSE])`

  * 4.0 이전에는 T가 기본, 4.0 부터는 F가 기본

* `as.data.frame(벡터 또는 행렬 등)`



---



### 인덱싱

* `[행의 인덱싱, 열의 인덱싱]`
* `[열의 인덱싱]` : 데이터프레임 구조 유지
* `df$컬럼이름`
* `[[열의 인덱싱]]`
* `subset(df, select = c(컬럼이름,컬럼이름,컬럼이름))`



---



### 데이터프레임 변환

* `cbind(df, 벡터)` : 열 연장
* `rbind(df, 벡터)` : 행 연장

* `df$컬럼이름 <- 연산`

  ```R
  df <- data.frame(var1=c(4,3,8), 
                   var2=c(2,6,1))
  df$var_sum <- df$var1 + df$var2
  ```

  

---



### 데이터프레임 구조 확인

* `str(df)`
* `dim(df)`



---



### 원하는 행과 열 추출

> `df(조건, c("컬럼명", "컬럼명", ...)`
>
> `subset(df, subset=(조건), select=c("컬럼명", "컬럼명", ...))`
>
> `subset(df, 조건, c("컬럼명", "컬럼명", ...))`

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



### 함수

* `colnames(df)`

  * `names(df)`

* `rownames(df)`

* `mean(df$컬럼이름)` : 컬럼에 대한  평균

* `isfelse(조건문, TRUE일때, FALSE일때)`

  ```R
  df <- data.frame(var1=c(4,3,8), 
                   var2=c(2,6,1))
  df$result <- ifelse(df$var1>df$var2, 
                      "var1이 크다", "var1이 작다")
  ```

  

---



### 데이터프레임 데이터 표 형식으로 보기

`View(df)`



---



### 특정 열 기준으로 정렬하기

`df[order(df$컬럼명),]`



---



### 함수

* `mean(df$컬럼이름)` : 해당 컬럼에 대한 전체 평균



---



### 데이터프레임 합치기

#### 열단위 합치기

* `cbind(df1. df2)`
* `bind_cols(df1, df2)`

#### 행단위 합치기

* `rbind(df1, df2)`
* `bind_rows(df1, df2)`

#### 조인

* basic R 에서는 `merge()`, dplyr 에서는 `join()` 제공

* basicR

  ```R
  merge(df1, df2)
  merge(df1, df2, all.x = T)
  merge(df1, df2, all.y = T)
  merge(df1, df2, all = T)
  ```

* dplyr 패키지

  ```
  XXXX_join(df1, df2, by="열이름")
  ```
  * 두 개의 데이터프레임을 선택된 공통의 변수(행 안의 변수, 항목)에 기반해 결합
  * 열 기준으로 붙임 (왼쪽에서 오른쪽으로)
  * basic R 에서는 `merge()`, dplyr 에서는 `join()` 제공
  * 결합하는 경우, 두 개의 인자의 위치에 따른 4가지 결합 기준을 이용할 수 있음
    * `left_join()`
      * 왼쪽 자료의 항목을 기준으로 결합
      * 왼쪽 자료와 동일한 항목이 없는 경우 NA로 채워짐
      * `merge(test1, test2, all.x = T)`
    * `right_join()`
      * 오른쪽 자료의 항목을 기준으로 결합
      * 오른쪽 자료와 동일한 항목이 없는 경우 NA로 채워짐
      * `merge(test1, test2, all.y = T)`
    * `inner_join()`
      * 두 자료의 공통 항목만을 결합
      * NA를 만들지 않음
      * `merge(test1, test2)`
    * `full_join()`
      * 두 자료의 모든 항목을 결합
      * 공통된 항목이 없는 경우 NA로 채워짐
      * `merge(test1, test2, all = T)`