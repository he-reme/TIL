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



### 매개변수에 전달된 데이터 타입 체크

#### 데이터 타입 체크 함수

* `is.vector(x)`
  
  * `list`도 포함됨
* `is.data.frame(x)`
* `is.list(x)`
  
  * `dataframe`도 포함됨
* `is.matrix(x)`
* `is.array(x)`
* `is.function(x)`
* `is.null(x)`

* 그래서... 포함되는 것 제외하고, 오로지 그 데이터 타입만을 체크하고 싶으면

  ```R
  f <- function(x){
    result <- NULL
    if(is.vector(x)  && !is.list(x)) result <-"벡터를 전달했군요!"
    else if(is.data.frame(x)) result <- "데이터프레임을 전달했군요!"
    else if(is.list(x)) result <- "리스트를 전달했군요!"
    else if(is.matrix(x)) result <- "매트릭스를 전달했군요!"
    else if(is.array(x)) result <- "배열을 전달했군요!"
    else if(is.function(x)) result <- "함수를 전달했군요!"
    return(result)
  }
  ```

#### 한번에 여러 요소 체크

* `is.xxx(v)` 는 한번에 1개의 요소 밖에 체크하지 못함
  * 제일 처음에 받은 index 1의 요소만 체크
* `any(is.xxx(v))` 는 여러 요소를 체크하고 하나라도 해당되면 `TRUE`를 반환
* `all(ix.xxx(v))` 는 여러 요소를 체크하고 모두 해당되면 `TRUE`를 반환



---



### 함수와 같이쓰는..

#### apply()

* `apply(m, 1, 함수)`
* `apply(m, 2, 함수)`
* `sapply(v, 함수)`
  * 심플 apply
  * 벡터가 가지고 있는 원소가 5개면 원소 하나당 호출되므로, 함수 5번 호출
    * 리턴값을 계속 모으고 있다가 마지막에 벡터 형식으로 한꺼번에 출력
  * 리턴값 : 가급적 단순한 객체
* `lapply(v, 함수)`
  * 리스트 apply
  * 리턴값 : 무조건 list 객체 

#### invisible()

* `return()` 함수와 같은 용도이지만, 함수 단독 호출 시에는 보이지 않음

```
f1 <- function(x) return(x+10)
f2 <- function(x) invisible(x+10)
f1(100) # 110
f2(100) # 리턴값 안보임
r1 <- f1(100); r1 # 110
r2 <- f2(100); r2 # 100 이러면 보임
```

#### sleep()

```R
f <- function(second){
	for(data in LETTERS[1:5]){
		cat(data)
		Sys.sleep(second)
	}
}
f(0) # 원래 함수 실행한 것처럼 나옴
f(1) # 1초마다 쉼
```



---



### 예외처리1

#### stop() 

* error 메시지 출력, 함수 강제 종료
* 빨간 메시지

* 예시

  ```R
  testError <- function(x){
    if(x<=0)
      stop("양의 값만 전달 하세요! 더 이상 수행 안할거임..")
    return(rep("테스트",x))
  }
  
  testError(5)
  testError(0)
  ```

#### warning()

* warning 메시지 출력,  함수 강제 종료하지는 않음.

* 보통 default 처리 해줌

* 빨간 메시지

* 예시

  ```R
  testWarn <- function(x){
    if(x<=0)
      stop("양의 값만 전달 하세요! 더 이상 수행 안할거임..")
    if(x>5){
      x<-5
      warning("5보다 크면 안됨!! 그래서 5로 처리함..")
    }
    return(rep("테스트",x))
  }
  
  testWarn(3)
  testWarn(10)
  ```

#### try()

* try 안의 구문에 에러나 경고가 발생해도 계속 실행함

```R
testError <- function(x){
  if(x<=0)
    stop("양의 값만 전달 하세요! 더 이상 수행 안할거임..")
  return(rep("테스트",x))
}
```

* 비교1

  ```R
  test <-function(p){
    cat("난 수행함\n")
    testError1(-1)
    cat("나 수행할 까요? \n") # 수행 안함
  }
  test()
  ```

* 비교2

  ```R
  test <- function(p){
    cat("난 수행함\n")
    try(testError(-1))
    cat("나 수행할 까요? \n") # 수행함
  }
  test()
  ```



---



### 예외처리2

#### tryCatch (warning - error - finally)

 ```
f <- function(p){
	tryCatch({
		# 정상수행, 경고, 에러 여부 확인
	},warning = function(w){
		print(w)
	},error = function(e){
		print(e)
	}, finally = {
		# 경고, 에러 발생 여부에 관계없이 반드시 수행되는 부분
	}
	)
}
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

```
f7 <- function(type, ...){
	return(switch(EXPR=type, paste0("A", c(...)), paste0("B", c(...)), 
			paste0("C", c(...)), paste0("D", c(....))))
}
f7(type=1, 100, 200, 300)
f7(1, 100, 200, 300)
```



---

