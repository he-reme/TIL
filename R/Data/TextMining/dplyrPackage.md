# dplyr 패키지

> 데이터프레임에 담겨진 데이터들의 전처리에 가장 많이 사용되는 패키지

* 데이터를 빨리 가공할 수 있도록 도와주는  R 패키지
* **데이터 전처리 작업**에 가장 많이 사용 되는 패키지
* 유연한 데이터 조작의 문법을 제공
* **데이터프레임을 집중적으로 다룸**

* C언어로 만들어짐

```R
install.packages("dplyr")
library(dplyr)
```

#### 데이터 전처리

* 분석에 적합하게 데이터를 가공하는 작업
* 유사한 말
  * 데이터 가공
  * 데이터 핸들링
  * 데이터 클리닝
* 데이터의 이상치나 결측치에 대한 처리도 이 단계에서 처리함.

#### dplyr 패키지 방식으로 코딩

* 기존에 R로 코딩했을 때

  `d <- f3(f2(f1(a)))`

* dplyr 패키지 방식으로 코딩하면

  `d <- a %>% f1 %>% f2 %>% f3`


#### `%>%`

* 왼쪽의 결과를 오른쪽 함수의 첫번째 인자로 넘김

#### linux 명령어

* OS (Operating System), 운영체제
  * 컴퓨터 HW가 실제 컴퓨터의 역할을 할 수 있으려면 운영체제라는 시스템 프로그램이 설치되어 있어야 한다.
  * windows 10, mac os, android os, ios, linux, unix
* AWS, 클라우드 환경의 시스템
  * linux
  * ls, rm, cd, pwd, grep, find ...
  * `ls | more`
    * `|` : 파이프 기호
      * 왼쪽 명령의 결과를 오른쪽 명령의 첫번째 인자로 넘김



---



## chain() 함수

> `%>%`
>
> 단축키는 [shift+ctrl+M]

* `chain()` 함수 혹은 간단히 `%>%`를 이용함으로써 각 조작을 연결해서 한 번에 수행할 수 있음
* `%>%` 를 사용했을 때
  * 가장 먼저 데이터프레임을 지정하면,
  * 그 다음부터의 첫번째 인자를 생략할 수 있을 수 있음
  * 그리고 앞선 함수의 결과(데이터프레임)를 뒤에 오는 함수의 입력 값으로 사용하게 됨

#### 예시

```R
df %>% filter(math > 50)
```

#### 가독성 높이는 법

* 체이닝이 길어질수록 가독성이 떨어지므로 줄바꿈을 해주자!

```R
df <- 함수1() %>%
	함수2() %>%
	함수3() %>%
	함수4() %>%
	함수5()
```

* 또한 대입을 오른쪽에 넣어주면 더 가독성이 높아진다 (취존)

```R
함수1() %>%
	함수2() %>%
	함수3() %>%
	함수4() %>%
	함수5() -> df
```



---



## 주요 함수

* `filter()`
  * 조건에 의한 row 데이터 부분집합 선별
* `slice()`
  * 위치를 사용한 row 데이터 부분집합 선별
* `arrange()`
  * 데이터프레임 행 정렬
* `select()`
  * 데이터프레임 변수 선별
  * `select(df, starts_with())`
  * `select(df, ends_with())`
  * `select(df, contains())`
  * `select(df, matchs())`
  * `select(df, one_of())`
  * `select(df, num_range())`
  * `select_if(df, 조건)`
* `pull()`
  * `select()` 는 데이터프레임의 구조를 유지시키고 선별하지만,
  * `pull()`은 **벡터 형식**으로 선별함
* `rename()`
  * 열 이름 재설정
* `distinct()`
  * 중복없는 유일한 행 추출
* `sample_n()`
  * 랜덤으로 특정 개수의 행 추출
* `sample_frac()`
  * 랜덤으로 특정 비율의 행 추출
* `mutate()`
  * 파생 열 생성 (새로운 열 추가)
  * 이미 만들어져 있는 열을 언급하는 것을 허락함
* `transmute()`
  * 새로운 열 생성
  * 꼭 새로운 열이어야 함 (???)
* `count()`
  * 전달된 데이터 프레임에서, 특정 열에 대하여 행 갯수 반환
  * 두번째 인자를 생략하는 경우, 모든 행에 대하여 반환
* `group_by()`
  * 그룹별로 묶기
* `summarise()`
  * 묶인 그룹에 대한 처리

* `bind_rows()`
* `bind_cols()`

* 조인

---



#### filter()

> 조건에 의한 선별

* `&` (AND) 조건으로 row 데이터 부분집합 선별

  ```R
  filter(dataframe, 조건1, 조건2, ...)
  ```

* `|` (OR) 조건으로 row 데이터 부분집합 선별

  ```R
  filter(dataframe, 조건1 | 조건2 | ...)
  ```

* 같이 사용하면 좋은 ...

  * `%in%`

    ```R
    filter(dataframe, 열이름 %in% 집합)
    ```

    * 해당 열의 변수 중 오른쪽 sequence 중에 하나에 해당되면 해당 행  추출

    * 예시

      ```R
      filter(df, class %in% c(1,3,5))
      ```



#### slice()

> 위치에 의한 선별

* 위치를 지정해서 row 데이터 부분집합 선별

  ```R
  slice(dataframe, from, to)
  ```

*  예시

  ```R
  slice(df, 6:10)
  ```



---



#### arrange()

* 데이터프레임 행 정렬

  ```R
  arrange(dataframe, 기준변수1, 기준변수2, ...)
  ```

* 여러개의 기준에 의해서 정렬하고 싶으면 기준 변수를 순서대로 나열

* 오름차순 정렬 : 기본 젖ㅇ렬 옵션

* 내림차순으로 정렬 : `desc()` 입력

* 예시

  ```R
  arrange(df, desc(기준변수1), 기준변수2)
  ```

  * 기준변수1을 기준으로 내림차순 정렬하고, 기준변수2를 기준으로 오름차순 정렬
  
* 같이 사용하면 좋은...

  * `head` : top 6

  * `head(n)` : top n

  * 예시

    ```R
    emp %>% arrange(desc(sal)) %>% 
      head(1)
    ```



---



#### select()

* 데이터프레임 열 선별

  ````R
  select(dataframe, 열이름1, 열이름2, ...)
  ````

  * 예시

    ```R
    select(df, 열이름1, 열이름2, 열이름3)
    select(df, 열이름1:열이름3)
    select(df, 1:3)
    select(df, -열이름1, -열이름2) # 열이름1, 열이름2를 제외한 추출
    ```

* `name` 으로 시작하는 모든 열 선별

  ```R
  select(dataframe, starts_with("name"))
  ```

  * 대소문자 구분 X

  * 대소문자를 구분하고 싶으면

    ```R
    select(dataframe, starts_with("name", ignore.case=F))
    ```

* `name` 으로 끝나는 모든 열 선별

  ```R
  select(dataframe, ends_with("name"))
  ```

* `name` 을 포함하는 모든 열 선별

  ```R
  select(dataframe, contains("name"))
  ```

* 정규 표현과 일치하는 문자열이 포함된 모든 열 선별

  ```R
  select(dataframe, matches("string"))
  ```

* 변수명 그룹에 포함된 모든 열 선별

  ```R
  변수명그룹 <- c("변수1", "변수2", ...)
  select(dataframe, one_of(변수명그룹))
  ```

* 접두사와 숫자 범위를 조합해서 열 선별

  ```R
  select(dataframe, num_range("접두사", x:y))
  ```

* 조건에 맞는 열 선별

  ```R
  select_if(df, 조건)
  ```

  


---



#### rename()

* 데이터프레임 변수 이름 변경

  ```R
  rename(dataframe, 새열이름1=옛열이름1, 새열이름2=옛열이름2, ...)
  ```



---



#### distinct()

* 중복없는 유일한 값 추출

  ```R
  distinct(dataframe, 기준열1, 기준열2, ...)
  ```



---



#### sample_n()

* 특정 개수만큼 무작위 표본 데이터 추출

  ```R
  sample_n(dataframe, 특정 개수)
  ```

* 특정 개수만큼 중복을 허용하는 무작위 표본 데이터 추출

  ```R
  sample_n(dataframe, 특정 개수, replace=T)
  ```

#### sample_frac()

* 특정 비율만큼 무작위 표본 데이터 추출

  ```R
  sample_frac(dataframe, 특정 비율)
  ```

  * 특정 비율 : 0 ~ 1



---



#### mutate()

* 파생 변수 추가 ( 새로운 열 추가 )

  ```R
  mutate(새로운열1=식1, 새로운열2=식2, ...)
  ```

  * `식`에 올 수 있는 것
    * 계산식
    * 리턴을 갖는 함수
    * 단일값

* 예시

  ```R
  score %>% mutate(총점=국어+영어+수학, 평균=총점/3)
  ```

  * 총점과 평균 열이 새로 추가됨

* 같이 사용하면 좋은 ...
  
  * `isfelse(조건식, "TRUE일 때 리턴값", "FALSE일 때 리턴값")`



---



#### count()

* 특정 열에 따른 그룹별로 행의 개수 반환

  ```R
  df %>% count(열이름)
  ```

* 모든 행의 개수 반환

  ```R
  df %>% count
  ```



#### tally()





---



#### group_by()

* 해당 열에 대해 같은 값을 갖는 것끼리 그룹으로 묶기

  ```R
  group_by(df, 열이름)
  ```

* 그룹 묶고, 한번 더 그룹 묶기

  ```R
  group_by(df, 열이름1, 열이름2) # 열이름1로 그룹 묶고 그 속에서 열이름2로 그룹 묶기
  ```

  

#### summarize()

* 묶인 그룹에 대한 요약 처리

  ```R
  summarize(df, 추가할열이름1=요약함수1, 추가할열이름2=요약함수2, ...)
  ```

* 자주 사용하는 요약 통계량 함수
  * `mean()` : 평균
  * `sd()` : 표준편차
  * `sum()` : 합계
  * `median()` : 중앙값
  * `min()` : 최솟값
  * `max()` : 최댓값
  * `n()` : 빈도

#### 같이 사용하면?

```
dataframe %>% group_by(열이름) %>% summarise(추가할열이름=요약함수)
```

* 그룹 단위로 모든 행 출력하기

  ```R
  df %>% group_by(열이름) %>% summarise(n=n())
  ```

* 예시 1

  ```R
  df %>% group_by(Manufacturer) %>% summarise(mean_price=mean(Price), max_price=max(Price), min_price=min(Price))
  ```

  ```R
  Manufacturer  mean_price  max_price  min_price
      a            10.1         20        5
      b            20.0         30        10
      c            15.5         25        10
  ```

* 예시 2

  ```R
  exam %>%
    group_by(class) %>%                   # class별로 분리
    summarise(mean_math = mean(math),     # math 평균
              sum_math = sum(math),       # math 합계
              median_math = median(math), # math 중앙값
              n = n())                    # 학생 수
  ```



---



#### 모든 행 개수 반환

```R
df %>% summarise(n=n())
df %>% tally()
df %>% count()
```

#### 그룹별로 모든 행 개수 반환

```R
df %>% group_by(열이름) %>% summarise(n=n())
df %>% group_by(열이름) %>% tally()
df %>% group_by(열이름) %>% count()
```



---



#### bind_rows()

* 두 개 이상의 데이터프레임을 행 기준(위에서 아래로)로 합칠 때 사용하는 함수

* 합치려는 데이터프레임들의 열 갯수가 동일해야 함

* `rbind()` 함수와 유사한 기능 수행

  ```R
  bind_rows(df1, df2, ...)
  ```

  

#### bind_cols()

* 두 개 이상의 데이터프레임을 열 기준(왼쪽에서 오른쪽으로)로 합칠 때 사용하는 함수

* 합치려는 데이터프레임들의 행 갯수가 동일해야 함

* `cbind()` 함수와 유사한 기능 수행

  ```R
  bind_cols(df1, df2, ...)
  ```

  

#### 특징

* 열이 서로 동일하지 않아도 행 기준으로 합칠 수 있음
* `id` 매개변수를 사용해 합쳐지기 전의 데이터프레임의 원천을 알 수 있음
* dplyr 패키지의 처리 속도가 기본 패키지인 `rbind()` 대비 상대적으로 빠름



---



#### 조인

```R
XXXX_join(df1, df2, by="열이름")
```

* 두 개의 데이터프레임을 선택된 공통의 변수(행 안의 변수, 항목)에 기반해 결합
* 열 기준으로 붙임 (왼쪽에서 오른쪽으로)
* basic R 에서는 `merge()`, dplyr 에서는 `join()` 제공
* 결합하는 경우, 두 개의 인자의 위치에 따른 4가지 결합 기준을 이용할 수 있음
  * `left_join()`
    * 왼쪽 자료의 항목을 기준으로 결합
    * 왼쪽 자료와 동일한 항목이 없는 경우 NA로 채워짐
    * `merge(test1, test2, all.x = T)`
  * `right_join()`
    * 오른쪽 자료의 항목을 기준으로 결합
    * 오른쪽 자료와 동일한 항목이 없는 경우 NA로 채워짐
    * `merge(test1, test2, all.y = T)`
  * `inner_join()`
    * 두 자료의 공통 항목만을 결합
    * NA를 만들지 않음
    * `merge(test1, test2)`
  * `full_join()`
    * 두 자료의 모든 항목을 결합
    * 공통된 항목이 없는 경우 NA로 채워짐
    * `merge(test1, test2, all = T)`



---



## 데이터 정제

> 결측치, 이상치 제거하기

* 결측치 : 빠진 데이터
* 이상치 : 이상한 데이터



---



### 결측치

* Missing Value
* 누락된 값, 비어있는 값
* 함수 적용 불가
* 분석 결과를 왜곡하므로 제거 후 분석해야 함
* 표기 : `NA`

#### 결측치 확인하기

```R
is.na(df)
```

#### 결측치 빈도 확인하기

```R
table(is.na(df))
table(is.na(df$열이름)) # 열이름별로 별측치 빈도 확인
```

#### 결측치 있는 행 제거하기

```R
df %>% filter(!is.na(scor))
```

#### 결측치 제외하고 함수 적용하기

```R
df %>% summarise(sum_math=sum(math, na.rm=T))
```

#### 결측치 다른 값으로 대체하기

```R
df$열이름 %>% ifelse(is.na(exam$math), NA대체값, exam$math) 
```



---



#### 결측치 확인하기 (2)

`complete.cases(df)`

* 결측치를 가진 행만 출력



---



### 이상치

* Outlier
* 정상범주에서 크게 벗어난 값

#### 이상치 확인하기

```
table(df$열이름)
```

#### 이상치 처리하기 (NA값으로 바꾸기)

```R
df$열이름 <- ifelse(해당열에 대한 이상치 조건, NA, df$열이름)
```

```R
df$sex <- ifelse(df$sex==3, NA, df$sex)
```

#### 이상치를 제외하고 분석하기

```R
df$열이름1 <- ifelse(열이름1에 대한 이상치 조건, NA, df$열이름1)
df$열이름2 <- ifelse(열이름2에 대한 이상치 조건, NA, df$열이름2)
df %>% 
	filter(!is.na(열이름1), !is.na(열이름2)) %>%
	# 이 뒤는 이상치 처리했으니 분석하면 됨~
```

