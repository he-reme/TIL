# 산점도

* **다중변수 데이터**에서 두 변수에 포함된 값들을 2차원 그래프상에 점으로 표현하여 
* 분포를 관찰할 수 있도록 하는 도구
* 2개의 변수 사이의 관계, 관련성을 파악할 수 있도록 하는 도구

#### 다중변수 데이터

* 내장데이터셋 `iris` 처럼
  * 5개의 주제에 대해 데이터를 모음
    * 꽃받침의 길이, 폭
    * 꽃입의 길이, 폭
    * 품종
* 여러 주제의 데이터를 하나로 모은 2차원 형태의 데이터 

* 주제 = 변수 = 열



---



##  두 변수 사이의 산점도

#### 산점도 그리기

```R
wt <-mtcars$wt                   # 중량 자료
mpg <- mtcars$mpg                # 연비 자료
plot(wt, mpg,                    # 2개 변수 (x축, y축)     
     main='중량-연비 그래프',       # 제목
     xlab='중량(WT)',             # x축 레이블
     ylab='연비(MPG)',            # y축 레이블
     col='red',                  # point의 color
     pch=19)                     # point의 종류 
```

* 내장 데이터 셋 `mtcars`에 있는 2개의 변수 사이의 관계에 대해 그린 산점도
  * 2개의 변수
    * `wt` : 중량
    * `mpg` : 연비
* `point` : 점

#### point 종류

<img src="C:\Users\H\Desktop\멀캠\R\scatterplot_point.jpg" style="zoom: 67%;" />



---



## 여러 변수들 간의 산점도

> 여러 변수들 간의 추세를 한눈에 파악 가능

* 산점도는 기본적으로 2개의 변수에 대해서 작성
* 따라서, 변수가 2개인 데이터의 경우
  * 2개씩 짝 지어서 산점도를 그리면 됨

#### 산점도 그리기

```R
vars <- c('mpg','disp','drat','wt')    # 대상 변수 
target <- mtcars[,vars]                # 대상 자료 생성  
head(target)
pairs(target,                          # 대상 자료     
      main='Multi plots') 
```

```R
vars <- c('mpg','disp','drat','wt')    # 대상 변수 
target <- mtcars[,vars]                # 대상 자료 생성  
head(target)
plot(target,                          # 대상 자료     
     main='Multi plots') 
```

* `pairs()` 또는 `plot()` 사용
* 자동으로 2개씩 짝지어서 산점도를 그려줌
  * **대각선**은 **변수명**을 나타냄



---



## 그룹 정보가 있는 2개 변수의 산점도

> 두 변수간의 관계뿐만 아니라 그룹 간 관계도 파악 가능

* 2개의 변수에 대한 산점도를 작성할 때
* 만일, 그룹 정보를 알고있다면
* 각 그룹별 관측값들을 다른 색깔과 점의 모양을 표시할 수 있음

#### 산점도 그리기

```R
iris_new <- iris[,3:4]                # 데이터 준비
levels(iris$Species)                  # 그룹 확인
group <- as.numeric(iris$Species)     # 그룹을 숫자로 표현 (= 점의 모양과 색)
group                                 # group 내용 출력
color <- c('red','green','blue')      # 점의 컬러 (그룹 숫자와 대응해 사용할 예정)
plot(iris_new, 
     main='Iris plot',
     pch=c(group),
     col=color[group]) 
```

* `iris$Species`
  * 팩터형 데이터
* `as.numeric(팩터형데이터)`
  * 팩터 타입의 데이터를 숫자로 바꾸는 역할
  * 1부터 순서대로 대응되어 변환됨

#### 범례 추가

```R
legend(x='bottomright',               # 범례의 위치  
       legend=levels(iris$Species),   # 범례의 내용
       col=c('red','green','blue'),   # 색 지정
       pch=c(1:3))                    # 점의 모양 
```

* 그래프를 그린 후 위의 코드를 추가하면 범례가 추가됨
* `legend()`
  * 산점도 위에 범례를 겹쳐 출력할 때 사용