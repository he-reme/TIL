# 데이터 전처리

> Data Preprocessing



---



### `apply` 계열 함수

> 벡터, 행렬, 또는 데이터 프레임에 임의의 함수를 적용한 결과를 얻기 위한 함수
>
> 데이터 전체에 함수를 한 번에 적용하는 벡터 연산을 수행
>
> 속도 빠르고, 구현도 간단

#### `apply()`

* 설명
  * 배열 또는 행렬에 주어진 함수를 적용한 뒤 그 결과를 벡터, 배열, 리스트로 반환
* 특징
  * 배열 또는 행렬에 적용
* 사용
  * `apply(데이터, 함수 적용 방향, 함수)`

#### `lapply()`

* 설명
  * 벡터, 리스트, 표현식에 함수를 적용하여 그 결과를 리스트로 반환
* 특징
  * 결과가 리스트
* 사용
  * `lapply(데이터, 함수)`

#### `sapply()`

* 설명
  * `lapply`와 유사하나 결과를 가능한 심플한 데이터셋으로 반환

* 특징

  * 결과가 심플 데이터셋
  * 함수가 길이가 1인 벡터를 리턴했는데, `NULL` 값이 없으면 벡터, 있으면 리스트로 반환

* 사용

  * `sapply(데이터, 함수)`

    * 데이터가 데이터 프레임이면, 열단위로 함수 호출

  * 함수에 인자가 데이터 이외에 더 있는 경우

    * `sapply(데이터, 함수, 매개변수)` 

    * 예시1

      ```R
      weight <- c(65.4, 55, 380, 72.2, 51, NA)
      height <- c(170, 155, NA, 173, 161, 166)
      gender <- c("M", "F","M","M","F","F")
      df <- data.frame(w=weight, h=height)
      
      f <- function(x, wt=T){
        ...
        return(r)
      }
      
      sapply(df$w, f, F)
      sapply(df$w, f, wt=F) # 키워드로도 가능
      ```

    * 예시2

      ```R
      flower <- c("rose", "iris", "sunflower", "anemone", "tulip")
      
      sapply(flower, function(d, n=5) if(nchar(d) > n) return(d))
      sapply(flower, function(d, n=5) if(nchar(d) > n) return(d), 3)
      sapply(flower, function(d, n=5) if(nchar(d) > n) return(d), n=4)
      ```

      

#### `tapply()`

* 설명

  * 벡터에 있는 데이터를 특정 기준에 따라 그룹으로 묶은 뒤, 각 그룹마다 주어진 함수를 적용하고 그 결과를 반환

* 특징

  * 데이터를 그룹으로 묶은 뒤 함수를 적용

* 사용

  * `tapply(데이터, 인덱스, 함수)`

* 예시1

  ```R
  gender <- c("M", "F","M","M","F","F")
  tapply(1:6, gender, sum)
  ```

  ```
   F  M
  13  8
  ```

* 예시2

  ```R
  weight <- c(65.4, 55, 380, 72.2, 51, NA)
  gender <- c("M", "F","M","M","F","F")
  tapply(df$w, gender, mean, na.rm=TRUE)
  ```

  ```
        F         M
  53.0000  172.5333
  ```

  

#### `mapply()`

* 설명

  * `sapply`의 확장된 버전으로, 여러 개의 벡터 또는 리스트를 인자로 받아서
  * 함수에 각 데이터의 첫째 요소들을 적용한 결과, 둘째 요소들을 적용한 결과, 셋째 요소들을 적용한 결과 등을 반환

* 특징

  * 여러 데이터셋의 데이터를 함수의 인자로 적용한 결과

* 사용

  * `mapply(함수, 가변인자)`

* 예시

  ```R
  mapply(paste, 1:5, LETTERS[1:5], month.abb[1:5])
  ```

  ```
  "1 A Jan" "2 B Feb" "3 C Mar" "4 D Apr" "5 E May"
  ```

  



---



### `apply()`

```R
apply(
	X, # 배열 또는 행렬
	MARGIN, # 함수를 적용하는 방향. 1: 행방향 / 2: 열방향
	FUNC # 적용할 함수
	[,na.rm=TRUE] # NA는 제외하고 계산
)
```

* 행렬의 행 또는 열 방향으로 특정 함수를 적용하는 데 사용
* 배열 또는 행렬에 함수 `FUNC`을 `MARGIN` 방향으로 적용하여 
* 반환값을 벡터, 배열, 리스트로 반환 
  * 데이터X의 데이터타입과 함수 FUNC의 반환 값에 따라 어느 것이 반환 될지 예상할 수 있음 
* 인자
  * `X` : 배열 또는 행렬
  * `MARGIN` : 함수를 적용하는 방향
    * 1 : 행 방향
    * 2 : 열 방향
  * `FUNC` : 적용할 함수

* 반환값

  * 벡터 : `FUNC`이 길이가 1인 벡터들을 반환한 경우
  * 행렬 : `FUNC`이 길이가 1보다 큰 벡터들을 반환한 경우
  * 리스트 : `FUNC`이 서로 다른 길이의 벡터를 반환한 경우

  