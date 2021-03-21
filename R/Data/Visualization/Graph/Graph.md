# 그래프

## 그래프 종류

* 막대그래프

* 히스토그램

* 다중그래프

* 원그래프

* 선그래프

* 박스그래프
* 산점도그래프



---



## 그래프 저장

#### 그려지는 그래프를 파일에 저장하는 방법

```R
png("원하는이름.png", height=500, width=500)
# 그래프를 그린다. 이 때는 RStudio 그래프 보는 창에서 확인 불가
dev.off()
```

#### 그래프를 그린 후, 파일에도 저장하는 방법

```R
# 그래프를 그린다. RStudio 그래프 보는 창에서 확인 가능
dev.copy(png, "원하는이름.png", height=500, width=500)
dev.off()
```

```R
# 그래프를 그린다. RStudio 그래프 보는 창에서 확인 가능
dev.copy(pdf, "원하는이름.pdf", height=500, width=500)
dev.off()
```

* `dev.off()` 는 파일 저장 종료



---



## 시각화 함수 종류

#### 고수준 함수

* `plot()`
* `boxplot()`
* `hist()`
* `pie()`
* `barplot()`

#### 저수준 함수

* `title()`
* `lines()`
* `axis()`
* `legend()`
* `points()`
* `text()`

#### 칼라팔레트 함수

* `rainbow()`
* `cm.colors()` : 하늘색과 보라색의 조합
* `topo.colors()` : 바다와 바닷가 색
* `terrain.colors()` : 우디한 색
* `heat.colors()` : 가을가을한 색
* `gray.colors()` : 검정, 회색

#### 포인트 모양 (pch)

* 0 ~ 25, 등등의 인자가 있음

#### 라인 타입 (Ity)

* 0 : blank
* 1 : solid
* 2 : dashed
* 3 : dotted
* 4 : dotdash
* 5 : longdash
* 6 : towdash