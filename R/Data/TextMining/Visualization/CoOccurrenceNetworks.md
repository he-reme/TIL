# 동시출현 네트워크

* 동시출현

  * 한 문장, 문단 또는 텍스트 단위에서 같이 출현한 단어를 가리킴
  * 단어의 연결성을 찾는 데 활용됨

* 동시출현 네트워크

  * 특정 텍스트 단위에서 공동으로 출현한 단어의 집합적 상호 연결을 표현하는 방식
  * 나타나는 단어를 모두 표시한 뒤, 둘 사이를 선으로 연결해 나가다 보면 단어의 네트워크를 만들 수 있음

  * `qgraph 패키지`의 `qgraph()` 함수를 사용

  

---



## 사용

#### 패키지

```R
install.packages("qgraph")
library(qgraph)
```

#### `qgraph()`

```R
qgraph(
	matrix, 
	labels=정점이름들,
	diag=F,
	layout='spring',
	edge.color='blue',
	vsize=log(diag(com)*800)
)
```



---



## 예제

```R
lunch <- c("커피 파스타 치킨 샐러드 아이스크림",
           "커피 우동 소고기김밥 귤",
           "참치김밥 커피 오뎅",
           "샐러드 피자 파스타 콜라",
           "티라무슈 햄버거 콜라",
           "파스타 샐러드 커피"
)
cps <- VCorpus(VectorSource(lunch))
tdm <- TermDocumentMatrix(cps, control=list(wordLengths = c(1, Inf)))
tdm

m <- as.matrix(tdm)
com <- m %*% t(m)  
com

# 시각화
install.packages("qgraph")
library(qgraph)

qgraph(com, labels=rownames(com), diag=F, 
       layout='spring',  edge.color='blue', 
       vsize=log(diag(com)*800))
```

