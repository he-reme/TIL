# 박스그래프

> = 상자수염그림

* 사분위수를 시각화하여 그래프 형태로 나타낸 것
* 데이터의 분포 형태를 포함한 다양한 정보를 전달하기 때문에
  * 단일변수 수치형 자료를 파악하는 데 자주 사용됨



---



## 박스그래프 설명

![박스 그래프 구조](C:\Users\H\Desktop\멀캠\R\boxplot.jpg)

* 최댓값, 최솟값
  * 정상 범위에 있는 관측값 중에서의 최솟값, 최댓값을 의미
* 중앙값
  * 2사분위수



---



## 박스그래프 작성

#### 박스그래프 그리기

```R
dist <- cars[,2]                      # 자동차 제동거리 (단위: 피트)
boxplot(dist, main='자동차 제동거리')
```

#### 박스그래프 정보 보기

```R
boxplot.stats(dist)
```

* 박스그래프는 데이터의 전반적인 분포를 이해하는 데는 도움이 되지만,
* 구체적으로 최솟값, 최댓값, 중앙값 등이 정확히 얼마인지는 알기 어려움.
* 이를 알기 위해서 사용하는 함수!! `boxplot.stats()`
* **리스트 형태** 출력
* 정보
  * `$stats`
    * 정상범위의 데이터 내에서 사분위수에 해당하는 값들을 표시
    * 5개의 값 (차례대로)
      * `최솟값` `1사분위수` `중앙값` `3사분위수` `최댓값`
  * `$n`
    * 데이터에 있는 관측값들의 개수
  * `$conf`
    * 중앙값에 관련된 신뢰 구간
  * `$out`
    * 특이값들의 목록을 저장
* **특이값**들만 추출
  
* `boxplot.stats(dist)$out`
  
* 폰트 적용

  * 다른 그래프들은 그래프 그릴 때 `family='폰트명'` 추가해서 폰트 적용 할 수 있지만

  * 박스그래프는 불가능

  * 방법 : 하나씩 그리면서 폰트 적용해야 함

    ```R
    data <- read.table("data/온도.txt", header=TRUE, sep=",")
    
    boxplot(data, axes=F) # 박스 그림만 추가
    axis(1, at=1:12, lab=names(data), family="maple") # x축 추가
    axis(2, at=seq(-5, 15, 5), family="dog") # y축 추가
    title("다양하게 폰트를 지정한 박스플롯", family="cat", cex.main=2) # 제목 추가 
    box() # 박스 틀 그리기
    ```

    

---



## 그룹이 있는 데이터의 박스그래프

* 그룹 간 데이터 분포 차이 확인 가능
* 단일변수 데이터 중에는 그룹 정보가 포함되어 있는 데이터도 있음
  * 예) 꽃잎의 길이 -- 그룹 정보 : 품종

#### 과정

* 데이터의 관측값들을 품종별로 나누기
* 품종 그룹별로 박스그래프 그리기
* 품종들 간 데이터의 분포가 어떻게 다른지 확인 가능

#### 박스그래프 그리기

```R
boxplot(Petal.Length~Species,            # 자료와 그룹 정보
        data=iris,                       # 자료가 저장된 자료구조
        main='품종별 꽃잎의 길이',          # 그래프의 제목    
        col=c('green','yellow','blue'))  # 상자들의 색
```

* 내장 데이터 셋 : `iris`
  * 열 종류
    * `Sepal.Length`
    * `Sepal.Width`
    * `Petal.Length`
    * `Petal.Width`
    * `Species`

* `y`축 

  * 값
  * `Petal.Length`

* `x` 축

  * 그룹명

  * 그룹별로 박스가 그려짐

  * `Species`

#### x축 순서 바꾸기

```R
test$hours <- factor(test$hours, levels = test$hours[1:12]) # x축에 나타낼 것 factor형으로 바꿔주기
boxplot(fluctuation~hours,            # 자료와 그룹 정보
        data=test,                       # 자료가 저장된 자료구조
        main='변동률 이상치 확인',          # 그래프의 제목    
        col=rainbow(12))  # 상자들의 색
View(test)
str(test)
```

