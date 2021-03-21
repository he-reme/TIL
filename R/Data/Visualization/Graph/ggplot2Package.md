# ggplot2 패키지

> 그래프 기능을 제공하는 패키지

```R
install.packages("ggplot2") # ggplot2 패키지 설치
library(ggplot2)
```

#### 구성요소

* A set of layers
  * Data
  * Aesthetic mappings (aes)
  * A geometric object (geom)
  * A statistical transformation (stat)
  * A position adjustment (position)
* A set of scales
  * 데이터 값이 에스테틱에 대입되는 과정을 조절
  * guide(축과 범례 등)가 어떻게 표시될지 결정
* A coordinate system
  * 좌표를 결정하는 에스테틱들이 어떻게 연결되는지를 결정
  * 기본값 : Cartesian 좌표평면
  * stat과 geom이 반영된 이후 변경할 수 있음
* A faceting specification



---



## A set of layers

#### Data

* 그래프를 그리려는 데이터
* 구조 : 데이터 프레임
* 데이터 기록 방식 : long-famat에 기반한 tidy data

#### Aesthetic Mapping

* 데이터의 요소와 그래프의 요소를 대응시키는 과정
* 그리려고 하는 그래프가 필수적으로 요구하는 대응요소만 만족시키면 됨
* 하나의 변수가 여러 가지 시각적 요소에 대응할 수도 있음

#### Geometric Object

* 어떤 형태의 그래프를 그릴지 지정
* geom 이라고 함

#### Position

* 그래프의 형태를 지정했으면 그래프에서 각 도형이 어떤 식으로 배치될 지를 결정
* 막대 그래프나 선 그래프일 경우, 누적 그래프를 그릴 때 position 옵션을 조정해서 형태를 변경할 수 있음

#### Statistical Transformation

* 마지막으로 값이 어떻게 그래프에 반영되는지 결정하는 옵션
* stat 라고 함
* 히스토그램과 같이 구간내에 존재하는 값의 개수를 세거나 밀도를 계산하는 등, 주어진 값을 변경시켜서 그래프에 반영시킬 때 사용

#### 기본사항

* 각 변수는 개별의 열로 존재
* 각 관측치는 행으로 구성
* 각 표는 각 하나의 관측 기준에 의해서 조작된 데이터를 저장
* 만약 여러 개의 표가 존재한다면, 적어도 하나이상의 열이 공유되어야 함



---



## 그래프 그리는 과정

#### 1. 배경 설정하기

```R
ggplot(data=df, aes(x=열이름1, y=열이름2))
```

#### 2. 그래프 추가하기

* 배경에 산점도 추가

  ```R
  ggplot(data=df, aes(x=열이름1, y=열이름2)) + geom_point()
  ```

#### 3. 축 범위를 조정하는 설정 추가하기

* x축 범위 3~6으로 지정

  ```R
  ggplot(data=df, aes(x=열이름1, y=열이름2)) +
  geom_point() + xlim(3,6)
  ```

* x축 범위 3~6, y축 범위 10~30으로 지정

  ```R
  ggplot(data=df, aes(x=열이름1, y=열이름2)) +
  geom_point() + xlim(3,6) + ylim(10, 30)
  ```

#### 4. 칼라와 점모양 추가하기

```R
ggplot(data=df, aes(x=열이름1, y=열이름2)) +
geom_point(shape=21, size=6, color='blue') + 
xlim(3,6) + ylim(10, 30)
# shape는 점모양 번호
```

#### 5. 열 별로 칼라 설정

```R
ggplot(data=df, aes(x=열이름1, y=열이름2, col=열이름3)) + geom_point()
```



---



## 그래프

```R
df <- df_data %>% group_by(열이름1) %>% summaris(mean_열이름2 = mean(열이름2))
```

#### 집계 막대 그래프

```R
ggplot(data=df, aes(x=열이름1, y=열이름2)) + geom_col()
```

* 빈도 막대 그래프와 다른 점 : y축 직접 지정

#### 빈도 막대 그래프

```R
ggplot(data=df, aes(x=열이름1)) + geom_bar()
```

* 자동으로 `x` 축으로 지정한 열의 빈도수를 계산해서 그려줌
* 그래서 `y` 축을 정해주면 에러남

#### 선 그래프

```R
ggplot(data=df, aes(x=열이름1, y=열이름2)) + geom_line()
```

#### 상자 그림

```R
ggplot(data=df, aes(x=열이름1, y=열이름2)) + geom_boxplot()
```

#### 산점도 그래프

```R
ggplot(data=df, aes(x=열이름1, y=열이름2)) + geom_point()
```



---



## 그래프 저장

* 정적 그래프로 저장 

  ```R
  # 그래프 그리기
  ggsave("이름.png")
  ```

  * 이미지 파일 형식 저장
  * ggplot2 패키지 내부 함수

* 인터랙티브 그래프로 저장

  ```R
  install.packages("plotly")
  library(plotly)
  # 그래프 그리기
  ggplotly(p)
  ```

  * html 파일 형식 저장
  * plotly 패키지 내부 함수
  * RStudio 에서는 Viewer 탭에서 확인 가능
  * 커서를 이용해서 인터랙티브하게 그래프를 사용할 수 있음
    * 점 마다의 정보 보기
    * 원하는 데이터만 보기





