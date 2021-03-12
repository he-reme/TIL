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
	vSize="열이름", 
	index=c("열이름1", "열이름2"), 
	title="트리맵 타이틀", 
	fontfamily.title="폰트명", 
	fontfamily.labels="폰트명")
```

* `vSize` : 양을 담는 열이름을 인자로 줘야 함
* `index` : 표현하고 싶은 계층 순서대로 벡터로 생성

#### 트리맵 저장

```R
dev.copy(png, "원하는이름.png")
dev.off()
```



---



* 더 많은 사용법은 RStudio - help 탭 참고!!!

