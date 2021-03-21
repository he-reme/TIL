# 방사형 차트

> = 레이더차트, 거미줄 차트

* 다중변수 데이터를 2차원 평면에 시각화함

#### 패키지

```R
install.packages('fmsb')
library(fmsb)
```



---



## 방사형 차트 작성

#### 데이터 준비

```R
score <- c(80, 60, 95, 85, 40)
max.score <- rep(100, 5)
min.score <- rep(0, 5)
ds <- rbind(max.score, min.score, score)
ds <- data.frames(ds)
colnames(ds) <- c('국어', '영어', '수학', '물리', '음악')
```

* 첫 번째 행, 두 번째 행에는 각 변수(열)의 범위가 입력되어야 함
  * 첫 번째 행 : 최댓값
  * 두 번째 행 : 최솟값

#### 방사형 차트 그리기

```R
radarchart(ds)
```

#### 매개변수 지정

```R
radarchart(ds,
		   pcol='다각형 선의 색',
		   pfcol='다각형 내부의 색',
		   plwd=3,
		   cglcol='거미줄의 색',
		   cglty=1,
		   cglwd=0.8,
		   axistype=1,
		   seg=4,
		   axislabcol='x축의 레이블 색',
		   caxislabels=seq(0, 100, 25))
```

* `plwd`
  * 다각형 선의 두께
* `cglty`
  * 거미줄의 타입
  * 선 타입.. `LineGraph.md` 에서 확인 가능
* `cgkwd`
  * 거미줄의 두께
* `axistype`
  * 축의 레이블 타입
  * `0` ~ `5`
    * `0` : 눈금에 레이블을 붙이지 않음 (기본값)
    * `1` : 차트 상단 중심축에만 레이블 표시
    * `2` ~ `5`  : 설명 생략
* `seg`
  * 축의 눈금 분할
* `caxislabels`
  * 축의 레이블 값