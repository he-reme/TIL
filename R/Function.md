# 함수

> R 프로그램의 주요 구성 요소로서 특정 작업을 독립적으로 수행하는 프로그램 코드 집합



---



### 함수 정의

```R
함수명 <- function([매개변수]){
	# 함수 수행 명령 문장들
	[return(리턴하려는값)]
}
```

* 리턴값

  * `return()` 함수 호출하여 처리
  * 리턴값이 없는 함수
    * 생략된 경우 마지막으로 출력된 데이터값이 자동으로 리턴됨
    * 가급적 리턴함수를 사용하여 명확히 구현한느 것이 필요

  * `NULL` 리턴 : `return()`

* 아규먼트

  * 타입을 제한하려는 경우 : `is.xxxx()` 함수 활용
    * `is.na()`
    * `is.charactor()`
  * 기본값을 갖는 매개변수 선언 가능
    * `exam <- function(x=1, y){}`
  * 개수와 타입을 가변적으로 처리 가능
    * `exam <- function(...){ nums <- c(...)}`

* 지역 변수와 전역 변수

  * 지역 변수 
    * 함수 안에서 만들어진 변수
    * 함수내에서만 사용 가능
  * 전역 변수
    * 함수 밖에서 만들어진 변수
    * 함수 내에서 전역 변수 값 변경 : 대입연산자로 `<<-` 사용

  

---



### 함수 호출

```R
변수명 <- 함수명()
변수명 <- 함수명(아규먼트)
함수명() ★★★
함수명(아규먼트) ★★★
```



---



### 예제

```R
f1 <- function(){
	print("TEST")
}
f1()
```

```R
f2 <- function(x=1){
	cat(x)
}
f2() # x=1
f2(2) # x=2
```

``` R
f3 <- function(x=1, y){
	cat(x, y)
}
f3(3) # x=1, y=3
f3(2,2) # x=2, y=2
```

```R
f4 <- function(...){
	data <- c(...)
	sum <- 0
	for(item in data){
		if(is.numeric(item))
			sum <- sum + item
        else
        	print(item)
	}
	return(sum)
}
f4(10, 20, 30)
f4(10, 20, "test", 30, 40)
```

```R
f5 <- function(...){
	data <- list(...)
	sum <- 0
	for(item in data){
		if(is.numeric(item))
			sum <- sum + item
		else
			print(item)
	}
	return(sum)
}
f5(10, 20, 30)
f5(10, 20, "test", 30, 40)
```

```R
f6 <- function(){
  L <- LETTERS
  l <- letters
  return(paste(L,l,sep=""))
}
f6()
```

