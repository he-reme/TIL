# 팩터

> factor

* 가능한 범주값(level) 만으로 구성되는 벡터

* like.. 갯수를 가진 집합?

  ```
  score <- c(1, 3, 2, 4, 2, 1, 3, 5, 1, 3, 3, 3)
  f_score <- factor(score)
  ```

  ```
  1 3 2 4 2 1 3 5 1 3 3 3
  Levels: 1 2 3 3 4 5
  ```

* `plot(f)` 
  * `plot()` : 그래프 그려주는 함수
  * 팩터를 그래프로 그리면 열(아래)이 레벨, 행(왼)이 갯수인 막대그래프가 그려짐
* level은 생성 시 넣었던 벡터의 집합



---



### 생성 방법

* `factor(벡터)`

* `factor(벡터[, levels=레벨벡터])`

  ```R
  week.korabbname <- c("일", "월", "화", "수", "목", "금", "토")
  day2 <- factor(data1, levels=week.korabbname)
  ```

  * 생성 시 레벨을 지정
  * 벡터에 해당 레벨과 같은 요소가 없을 시 갯수는 0으로 보여짐
  * **유의사항**
    * level에 없는 벡터의 요소가 factor 생성시에 사용될 경우
    * `NA` 데이터가 됨

* `factor(벡터[, levels=레벨벡터], ordered=TRUE)`

* `factor(벡터[, levels=레벨벡터, labels=라벨벡터])`

  ```R
  gender <- factor(c(1,2,1,1,1,2,1,2), 
                   levels=c(1,2), 
                   labels=c("남성", "여성"))
  ```

  * 레벨1은 남성
  * 레벨2는 여성

  

---



### 레벨 정보 추출

`levels(팩터변수)`



---



### 함수

* `summary(f)` : 위에는 레벨, 아래는 갯수 반환

  ```R
  score <- c(1, 3, 2, 4, 2, 1, 3, 5, 1, 3, 3, 3)
  f_score <- factor(score)
  ```

  ```R
  1 2 3 4 5
  3 2 5 1 1
  ```

* `levels(f)` : 레벨만 반환

  