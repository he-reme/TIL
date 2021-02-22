# 행렬

* **2차원** 벡터
* 동일 타입의 데이터만 저장 가능



---



### 인덱싱

* `[행의 인덱싱, 열의 인덱싱]`
* `[행의 인덱싱,]`
* `[, 열의 인덱싱]`
* `drop` 속성 : 행렬 구조 유지 여부



---



### 생성 방법

* `matrix(data=벡터, nrow=행의갯수, ncol=열의갯수)`
* `matrix(data=벡터, nrow=행의갯수, ncol=열의갯수, byrow=TRUE)`
  * **열 먼저** 채우는게 디폴트
* `rbind(벡터들..)` : 행 연장
* `cbind(벡터들..)` : 열 연장



---



### 주요 함수

* `dim(m)` : 행렬이 몇차원인지 체크
* `nrow(행렬)` : 행 갯수
* `ncol(행렬)` : 열 갯수
* `rownames(m)` : 행 이름 부여
* `colnames(m)` : 열 이름 부여
* `rowSums(m)`
* `colSums(m)`
* `rowMeans(m)`
* `colMeans(m)`
* `sum(m)`
* `min(m)`
* `max(m)`
* `mean(m)`
* `apply(m, 1 또는 2, 함수)`

