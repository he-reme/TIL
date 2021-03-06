# 행렬

* **2차원** 벡터
* 동일 타입의 데이터만 저장 가능



---



### 생성 방법

> 열 먼저 채움

* `matrix(data=벡터, nrow=행의갯수, ncol=열의갯수)`

* `matrix(data=벡터, nrow=행의갯수, ncol=열의갯수, byrow=TRUE)`

  * 행 먼저 채우고 싶을 때 `byrow=TRUE` 사용

* `rbind(벡터들..)` : 행 연장, 행 이름도 해당 벡터들로 지정됨

  ```R
  vec1 <- c(1,2,3)
  vec2 <- c(4,5,6)
  vec3 <- c(7,8,9)
  mat1 <- rbind(vec1, vec2, vec3)
  ```

  ```
  1 2 3
  4 5 6
  7 8 9
  ```

* `cbind(벡터들..)` : 열 연장, 열 이름도 해당 벡터들로 지정됨

  ```R
  vec1 <- c(1,2,3)
  vec2 <- c(4,5,6)
  vec3 <- c(7,8,9)
  mat1 <- cbind(vec1, vec2, vec3)
  ```

  ```R
  1 4 7
  2 5 8
  3 6 9
  ```

  

---



### 인덱싱

```
m[1,1]
m[3,4]
```

* `[행의 인덱싱, 열의 인덱싱]`
* `[행의 인덱싱,]`
* `[, 열의 인덱싱]`

* `drop` 속성 : 행렬 구조 유지 여부

  ```
  mat[1,1,drop=F]
  mat[2,,drop=F]
  mat[,3,drop=F]
  ```

  * `drop=F` : 구조 지켜서 출력

  

---



### 주요 함수

* `dim(m)` : 행렬이 몇차원인지 체크 (행갯수, 열갯수 반환)

* `nrow(행렬)` : 행 갯수

* `ncol(행렬)` : 열 갯수

* `rownames(m)` : 행 이름 부여

* `colnames(m)` : 열 이름 부여

* `rowSums(m)` : 행 마다의 합

* `colSums(m)` : 열 마다의 합

* `rowMeans(m)`

* `colMeans(m)`

* `sum(m)` : 모든 요소의 합

  * `sum(m[행번호,])` : 해당 행의 합

  * `sum(m[,열번호])` : 해당 열의 합

* `min(m)` : 요소들 중 최소

  * `min(m[행번호,])` : 해당 행의 최소

  * `min(m[,열번호])` : 해당 열의 최소

* `max(m)` : 요소들 중 최대

  * `max(m[행번호,])` : 해당 행의 최대

  * `max(m[,열번호])` : 해당 열의 최대

* `mean(m)` : 모든 요소들의 평균

  * `sum(m[행번호,])` : 해당 행의 평균

  * `sum(m[,열번호])` : 해당 열의 평균

* `summary(m)` : 요소들의 연산 집합

* `apply(m, 1 또는 2, 함수)`

  * 1, 2에 따른 함수 실행
  * `1` : 행
  * `2` : 열
  * `함수` : `sum` `min` `max` `mean` 



---



### 연산

* `+` `-` `*` `/` 

* 모든 요소에 대해 연산 수행

  ```R
  m <- matrix(1:8, nrow=2)
  m <- m*3
  ```

  * 처음

    ```
    1 3 5 7
    2 4 6 8
    ```

  * 연산 수행 후

    ```
    3 9  15 21
    6 12 18 24
    ```

    