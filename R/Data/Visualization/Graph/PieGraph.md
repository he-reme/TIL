# 원그래프

* 하나의 원 안에 데이터값이 차지하는 비율을 넓이로 나타낸 그래프
* **도수분포표**로부터 쉽게 원그래프 작성 가능



---



## 원그래프 작성

#### 도수분포 계산

```R
data <- c('WINTER', 'SUMMER', 'SPRING', 'SUMMER', 'SUMMER',
              'FALL', 'FALL', 'SUMMER', 'SPRING', 'SPRING')
ds <- table(data)
```

* `table()`
  * 도수분포 계산

#### 원그래프 그리기

```R
pie(ds,
	main='원그래프 제목',
	col='색'
    labels=names(ds)
	radius=반지름크기)
```

* `col`
  * 색 지정
  * `c('brown', 'green', 'red', 'black', ...)`
  * 등등
* `labels`
  * 구간별 이름 표시
* `radius`
  * `-1` ~ `1`
  * 보통 `1`로 지정



---



## 3D 원그래프 작성

#### 패키지

```R
install.packages('plotrix')
library(plotrix)
```

#### 3D 원그래프 그리기

```R
ie3D(ds, 
     main='제목',
     labels=names(ds),                              
     labelcex=1.0,                                 
     explode=0.1,                                   
     radius=1.5,                                    
     col=c('brown','green','red','yellow'))      
```

* `labels`
  * 레이블 지정
* `labelcex`
  * 레이블 폰트 크기 지정
* `explode`
  * 간격 지정
* `radius`
  * 원 반지름 
* `col`
  * 색 지정