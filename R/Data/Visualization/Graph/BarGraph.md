# 막대그래프

> 그룹별로 집계된 데이터를 표현하는 도구

* '브랜드별 선호도'나 '연도별 쌀 생산량'과 같이 그룹이나 범주가 정해져 있는 데이터를 시각화하는 데 사용됨
* 각 막대는 특정 범주와 그룹(브랜드, 연도)을 나타내고, 각 막대의 높이는 범주나 그룹별로 집계한 데이터의 크기(선호, 비율, 생산량)를 나타냄

#### 목차

* 막대그래프 작성
* 중첩 그룹의 막대그래프

---



## 막대그래프 작성

#### 그룹별로 데이터 집계

```R
ds <- table(data)
```

* 막대그래프를 작성하기 위해서는 먼저 범주형 데이터를 그룹별로 데이터를 집계하는 작업이 필요함

* `table()`
  * 벡터에 저장된 범주형 데이터에 대해 데이터값이 종류별로 몇 개인지 계산하는 함수
  * like **도수분포 계산**

#### 막대그래프 그리기

```R
barplot(도수분포표, 
	main='막대그래프제목', 
    col.main='색',
	col='색', 
	xlab='x축설명', 
	ylab='y축설명',
	horiz=T,
	names=c(x축의 그룹 이름),
	cex.names=0.8,
    cex.axis=0.8
)
```

* `barplot()`
  * `도수분포표` : 그래프로 표현할 도수분포표 지정
  * `main` : 막대그래프 상단의 그래프 제목(타이틀)을 지정
  * `col` : 막대의 색 
    * `col.main` : 타이틀 색 지정
  * `xlab` : x축 값들이 무엇을 의미하는지 설명 (이름)
  * `ylab` : y축 값들이 무엇을 의미하는지 설명 (이름)
  * `horiz` : T (막대그래프를 수평 방향으로 출력) , F (기본값, 수직 방향)
  * `names` : x축의 그룹 이름을 변경
  * `las` : x축의 그룹 이름을 수직 방향으로 출력
    * 0 : 축 방향 (기본값)
    * 1 : 수평 방향 (축 방향에 상관 없음)
    * 2 : 축을 기준으로 수직 방향
    * 3 : 수직 방향 (축 방향에 상관 없음)
  * `ces` : 폰트 크기 지정
    * `ces.names` : x 축 폰트 크기
    * `ces.axis` : y 축 폰트 크기 
* 결과
  * x축 : 사계절 이름들
  * y축 : 빈도

#### 막대 색 지정

* 지정방법 3가지
  * 색의 이름
    * `'blue'`, `'red'`, `'yellow'`
  * 색상 코드
    * `'#0000FF'`
  * 색의 조합 
    * `rgb(빨강, 초록, 파랑, 투명도)` 
    * `rgb(0, 0, 0, 255, maxColorValue=255) `
* `colors()` 
  * 해당 함수를 실행하면 R 그래프에 사용할 수 있는 색 이름 확인 가능
* 막대별로 색 다르게 지정
  * 막대가 4개이면
  * 직접 지정
    * `col=c('blue', 'red', 'green', 'yellow')`
  * 팔레트를 통한 지정
    * `col=rainbow(4)`
    * 찾아보면 유사 함수 더 있음..

#### 예제

* 도수분포

  ```R
  favorite <- c('WINTER', 'SUMMER', 'SPRING', 'SUMMER', 'SUMMER',
                'FALL', 'FALL', 'SUMMER', 'SPRING', 'SPRING') # 범주형 데이터
  ds <- table(favorite) # 도수분포 계산 및 도수분포표 저장
  ds       
  ```

* 기본 막대 그래프 작성

  ```R
  barplot(ds, main='favorite season')
  ```

* 막대 색 지정

  ```R
  barplot(ds, main='favorite season', col='blue')
  ```

  ```R
  barplot(ds, main='favorite season', 
          col=c('blue','red','green','yellow')) 
  ```

  ```R
  barplot(ds, main='favorite season', 
          col=rainbow(4))
  ```

* x축, y축 설명

  ```R
  barplot(ds, main='favorite season', 
          col='green',                           
          xlab='계절',                         
          ylab='빈도수' )
  ```

* 막대 세로 방향 출력

  ```R
  barplot(ds, main='favorite season', 
          col='yellow',                       
          horiz=TRUE)
  ```

* x축의 그룹 이름 바꾸어 출력

  ```R
  barplot(ds, main='favorite season', 
          col='yellow',                         
          names=c('FA','SP','SU','WI'))
  ```

* 그룹 이름을 수직 방향으로

  ```R
  barplot(ds, main='favorite season', 
          col='green',                         
          las=2)        
  ```

  

---



## 중첩 그룹의 막대그래프

> 그루 안에 또 다른 그룹이 존재하는 경우

#### 상황 제시

* 인구 추정 데이터에서
* 연도를 기준으로 그룹이 나누어져 있고, 
* 연도 안에서 연령대별로 3개의 그룹이 존재하는 경우

```R
age.A <- c(13709, 10974, 7979, 5000, 4250)
age.B <- c(17540, 29701, 36209, 33947, 24487)
age.C <- c(991, 2195, 5366, 12980, 19007)

ds <- rbind(age.A, age.B, age.C)
colnames(ds) <- c('1970','1990','2010','2030','2050')  
```

#### 연도 별로 막대 만들기

```R
# 그래프의 작성
barplot(ds, main='인구 추정') 

# 연령대(A, B, C) 별로 색 다르게 지정하기
barplot(ds, main='인구 추정',
       col=c('green', 'blue', 'yellow'))
```

#### 연도 별 막대를 만들되, 연령대 또한 각각의 막대로 표현하기

```R
barplot(ds, main='인구추정',
       col=c('green', 'blue', 'yellow'),
       beside=T)
```

#### 범례 추가

* 중첩 그룹의 막대그래프의 경우 어느 막대가 무엇을 의미하는 지 그래프만 보고 파악하기 어려움

* 따라서 이를 설명해주는 범례 추가해주면 좋음

* **그래프 위에 범례를 표시 방법**

  ```R
  barplot(ds, main='인구추정',
         col=c('green', 'blue', 'yellow'),
         beside=T,
         legend.text=T)
  ```

  * `legend.text`
    * `T` 로 설정 시 : 행이름으로 자동 표시
    * `벡터`로 지정시 : 원하는 이름으로 행 순서대로 표시됨

* **그래프 밖에 범례 표시 방법**

  ```R
  par(mfrow=c(1, 1), mar=c(5, 5, 5, 7)) # 그래프 윈도우 설정
  
  barplot(ds, main='인구 추정', 
          col=c('green','blue','yellow'),
          beside=TRUE,
          legend.text=c('0~14세','15~64세','65세 이상'),
          args.legend = list(x='topright', bty='n', inset=c(-0.25,0)))
  
  par(mfrow=c(1, 1), mar=c(5,4,4,2)+0.1) # 그래프창 설정 해제
  ```

  * 위 그래프의 범례 
    * 제일 높은 막대 그래프에 맞춰 오른쪽으로 선을 그었을 때
    * 막대 그래프 오른쪽,  해당 선의 아래 오른쪽에 그려짐.
  * `par()`
    * 그래프를 표시할 창에 대해 설정하는 역할을 하는 함수
    * `mfrow=c(1,1)`
      * 그래프를 출력할 창을 어떻게 분할할 지 지정
      * `c(1,1)`은 창을 분할하지 않음을 의미
    * `mar=c(5, 5, 5, 7)`
      * 그래프를 출력할 창과 그래프 출력 영역 밖의 여유 공간을 지정
      * 숫자가 커질수록 여유 공간이 넓어짐
      * 기본값 : `c(5.1, 4.1, 4.1, 2.1)`
      * `c(bottom, left, top, right)`
  * `args.legend`
    * 여러 개의 사항을 `list()` 함수로 묶어서 지정할 수 있음 
      * `x='topright'`
        * 범례를 출력할 기본 위치를 지정
        * `toright` : 그래프 출력 영역의 위쪽에서 오른쪽을 의미
      * `bty='o'`
        * 범례가 표시되는 영역에 테두리선을 표시할지의 여부를 지정
        * `o` : 테두리선 표시 O
        * `n` : 테두리선 표시 X
      * `inset=c(-0.25, 0)`
        * 범례를 x축과 y축 방향으로 얼마나 이동시킬지를 지정
        * `-1` ~ `1` 사이의 값을 지정 (%를 의미)
        * x축의 `-` 는 오른쪽
        * 일반적으로 이 설정을 사용하는 듯

