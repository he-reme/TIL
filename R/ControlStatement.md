# 제어문

* 제어문을 적용하여 수행하려는 명령이 여러 개이면 블록`{}`로 구성

#### 목차

* if 문
* if else 함수
* switch 함수
* for 문
* while 문
* reqeat 명령문
* 분기문



---



## 조건문

### if 문

```R
if(조건1){
	# 수행 명령 문장
} 
else if(조건2){
	# 수행 명령 문장
}
else{
	# 수행 명령 문장
}
```



### ifelse 함수

```R
ifelse(조건, 조건이 참을 때 명령문, 조건이 거짓일 때 명령문)
```

* 예시

  ```R
  name <- c("Potter", "Elsa", "Gates", "Wendy", "Ben")
  gender <- factor(c("M", "F", "M", "F", "M"))
  math <- c(85, 76, 99, 88, 40)
  df <- data.frame(name, gender, math)
  df
  df$stat <- c(76, 73, 95, 82, 35)
  df$score <- df$math + df$stat
  df$grade <- ifelse(df$score>=150, "A",
                      ifelse(df$score>=100, "B",
                             ifelse(df$score>=70, "C", "D")))
  df
  ```



### switch 함수

```R
switch(EXPR=수치데이터, 식1, 식2, 식3, ...)
switch(EXPR=문자열데이터, 비교값1=식1, 비교값2=식2, 비교값3=식3, ...)
switch(EXPR=문자열데이터, 비교값1=, 비교값2=, 비교값3=식1, ...)
switch(EXPR=문자열데이터, 비교값1=식1, 비교값2=식2, 비교값3=식3, default식)
```

* 부등호 사용 불가

* 예시1

  ```R
  month <- sample(1:12,1)
  month <- paste(month,"월",sep="") # "3월"  "3 월"
  result <- switch(EXPR=month, "12월"=,"1월"=,"2월"="겨울", "3월"=,"4월"=,"5월"="봄", "6월"=,"7월"=,"8월"="여름", "가을")
  cat(month,"은 ",result,"입니다\n",sep="")
  ```

  ```R
  num <- sample(1:10,1)
  result = switch(EXPR = num,"A","B","C","D")
  result
  ```

* 예시2

  * score의 값이 90~100이면, level 변수에 "A등급" 저장
  * score의 값이 80~89이면, level 변수에 "B등급" 저장
  * score의 값이 70~79이면, level 변수에 "C등급" 저장
  * score의 값이 60~69이면, level 변수에 "D등급" 저장
  * score의 값이 59 이하면, level 변수에 "F등급" 저장

  ```R
  score <- sample(0:100, 1)
  score <- score%/%10 # 10으로 나눈 몫
  score <- as.character(score) # 문자열데이터로 변환
  grade <- switch(EXPR=score, "10"=, "9"="A", "8"="B", "7"="C", "6"="D", "F")
  grade
  ```

  

---



## 반복문

>  반복문 내에서 화면에 결과 출력을 하기 위해서는 출력함수(`print()`, `cat()`)를 사용해야 함



### for 문

```R
for(변수 in 데이터셋){
	# 수행 명령 문장
}
```

* 예시

  ```R
  for(i in 5:15){
  	# 수행 명령 문장
  }
  ```

  ```R
  scores <- c(10, 50, 100, 70)
  for(score in scores){
  	print(score)
  }
  ```

  

### while 문

```R
while(조건){
	# 수행 명령 문장
}
```



### reqeat 명령문

```R
rpeat{
	# 수행 명령 문장
	if(조건)
		break
}
```



* `while(TRUE)`와 동일
* 적어도 한 번 이상 명령문을 실행
* 무한 루프에서 벗어나기 위해 분기문을 반드시 포함해야 함



---



## 분기문

* `break`
  * 해당 루프(반복문)을 종료
* `next`
  * 현재 반복을 종료하고 실행 위치를 다음 반복문으로 이동
  * like `continue`
* 반복문 내에서 화면에 결과 출력을 하기 위해서는 출력함수(`print()`, `cat()`)를 사용해야 함