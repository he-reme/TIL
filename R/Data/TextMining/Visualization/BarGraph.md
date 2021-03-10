# 막대그래프

> 그룹별로 집계된 데이터를 표현하는 도구

* '브랜드별 선호도'나 '연도별 쌀 생산량'과 같이 그룹이나 범주가 정해져 있는 데이터를 시각화하는 데 사용됨
* 각 막대는 특정 범주와 그룹(브랜드, 연도)을 나타내고, 각 막대의 높이는 범주나 그룹별로 집계한 데이터의 크기(선호, 비율, 생산량)를 나타냄

#### 목차

* 막대그래프 작성
* 막대그래프 색 지정
* x축, y축에 설명 붙이기
* 막대그래프 방향 바꾸기
* 

---



## 막대그래프 작성

#### 그룹별로 데이터 집계

* 막대그래프를 작성하기 위해서는 먼저 범주형 데이터를 그룹별로 데이터를 집계하는 작업이 필요함

* `table()`
  * 벡터에 저장된 범주형 데이터에 대해 데이터값이 종류별로 몇 개인지 계산하는 함수
  * like **도수분포 계산**

#### 막대그래프 그리기

```
barplot(도수분포표, 
	main='막대그래프제목', 
	col='색', 
	xlab='x축설명', 
	ylab='y축설명',
	horiz=T,
	names=c(x축의 그룹 이름)
)
```

* `barplot()`
  * `도수분포표` : 그래프로 표현할 도수분포표 지정
  * `막대그래프제목` : 막대그래프 상단의 그래프 제목(타이틀)을 지정
  * `색` : 막대의 색 
  * `xlab` : x축 값들이 무엇을 의미하는지 설명 (이름)
  * `ylab` : y축 값들이 무엇을 의미하는지 설명 (이름)
  * `horiz` : T (막대그래프를 수평 방향으로 출력) , F (기본값, 수직 방향)
  * `names` : x축의 그룹 이름을 변경
  * `las` : x축의 그룹 이름을 수직 방향으로 출력
    * 0 : 축 방향 (기본값)
    * 1 : 수평 방향 (축 방향에 상관 없음)
    * 2 : 축을 기준으로 수직 방향
    * 3 : 수직 방향 (축 방향에 상관 없음)
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

  ```
  favorite <- c('WINTER', 'SUMMER', 'SPRING', 'SUMMER', 'SUMMER',
                'FALL', 'FALL', 'SUMMER', 'SPRING', 'SPRING') # 범주형 데이터
  ds <- table(favorite) # 도수분포 계산 및 도수분포표 저장
  ds       
  ```

* 기본 막대 그래프 작성

  ```
  barplot(ds, main='favorite season')
  ```

* 막대 색 지정

  ```
  barplot(ds, main='favorite season', col='blue')
  ```

  ```
  barplot(ds, main='favorite season', 
          col=c('blue','red','green','yellow')) 
  ```

  ```
  barplot(ds, main='favorite season', 
          col=rainbow(4))
  ```

* x축, y축 설명

  ```
  barplot(ds, main='favorite season', 
          col='green',                           
          xlab='계절',                         
          ylab='빈도수' )
  ```

* 막대 세로 방향 출력

  ```
  barplot(ds, main='favorite season', 
          col='yellow',                       
          horiz=TRUE)
  ```

* x축의 그룹 이름 바꾸어 출력

  ```
  barplot(ds, main='favorite season', 
          col='yellow',                         
          names=c('FA','SP','SU','WI'))
  ```

* 그룹 이름을 수직 방향으로

  ```
  barplot(ds, main='favorite season', 
          col='green',                         
          las=2)        
  ```

  

---



## 중첩 그룹의 막대 그래프



