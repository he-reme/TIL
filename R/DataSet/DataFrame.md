# 데이터프레임

> data.frame

* 2차원 구조
* 열단위로 서로다른 타입의 데이터들로 구성 가능
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
    클래스=c(1,1,2,2))
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

* `rbind(df, 벡터)` : 열 연장
* `cbind(df, 벡터)` : 행 연장

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

`subset(df, select=컬럼명들, subset=(조건))`



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