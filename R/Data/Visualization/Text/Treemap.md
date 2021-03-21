# 트리맵

> 기준 열을 지정하고, 양에 따라 네모칸으로 나눠 시각적으로 보여줌

#### 패키지

```
install.packages("treemap")
library(treemap)
```

#### 사용

```R
treemap(sales_df, 
	vSize="타일의 크기를 결정하는 열이름", 
    vColor='타일의 색상을 결정하는 열이름',
    type='타일의 컬러링 방법',
    bg.labels='yellow',
	index=c("열이름1", "열이름2"), 
	title="트리맵 타이틀", 
	fontfamily.title="폰트명", 
	fontfamily.labels="폰트명")
```

* `vSize` 
  * 해당 열의 값에 따라 타일의 크기를 결정
  * 양을 담는 열이름을 인자로 줘야 함
* `vColor`
  * 타일의 색
* `type`
  * 타일 컬러링 방법
    * `value`
      * `vColor`에서 지정한 열에 저장된 값의 크기에 의해 색이 결정됨
    * `index`
    * `comp`
    * `dens` 
    * 등등
* `bg.labels`
  * 레이블의 배경색
* `index` 
  * 표현하고 싶은 계층 순서대로 벡터로 생성

#### 트리맵 저장

```R
dev.copy(png, "원하는이름.png")
dev.off()
```



---



## 예시 그림

![](C:\Users\H\Desktop\멀캠\R\treemap.PNG)



---



... 더 많은 사용법은 RStudio - help 탭 참고!!!