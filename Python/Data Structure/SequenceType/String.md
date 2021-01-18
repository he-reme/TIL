# 문자열

> `str = "hello"`
>
> 불변
>
> 시퀀스형



---



## 사용 시 주의사항

* `str[0] = "n"`
  * **사용불가!!** 문자열은 불변형이기 때문에 위와 같이 값을 수정할 수 없음

* 인덱싱, 슬라이싱 가능



---



## 함수

### (1) `len(문자열)`

* 문자열 길이 반환

* `len(str)`



---



## 메서드

> 클래스에 소속된 함수
>
> 객체에 대해 특화된 작업 수행
>
> `문자열.메서드()`



### (1) 검색

> `str = "python programming"`

* `str.find('o')    #4`
  * `문자열 'o'`  를 찾아 위치 반환 : 4
  * **못찾으면 `-1` 반환**
* `str.rfind('o')`    
  * `문자열 'o'` 를 오른쪽부터 찾아 위치 반환 : 9
* `str.index('r')`
  * `문자열 'r'` 를 찾아 인덱스 반환 : 8
  * **못찾으면 `error`**

* `str.count('n')`
  * `문자열 'n'` 의 갯수 반환 : 2



### (2) 조사

> `str = "python programming"`

* `in` 구문
  * 특정 문자 유무 여부 조사
  * `'n' in str`
    * True

* `isalpha`
  * **모든 문자**가 **알파벳**인지 조사
* `islower`
  * **모든 문자**가 **소문자**인지 조사
* `isupper`
  * **모든 문자**가 **대문자**인지 조사
* `isspace`
  * **모든 문자**가 **공백**인지 조사
* `isalnum`
  * **모든 문자**가 **알파벳 또는 숫자**인지 조사
* `isdecimal`
  * **모든 문자**가 **숫자**인지 조사
* `isdigit`
  * **모든 문자**가 **숫자**인지 조사
* `isnumeric`
  * **모든 문자**가 **숫자**인지 조사
* `isidentifier`
  * **명칭으로 쓸 수 있는 문자**로만 구성되어 있는지 조사
* `isprintable`
  * **인쇄 가능한 문자**로만 구성되어 있는지 조사



### (3) 변경

#### [ 소문자, 대문자 ]

>  `str = "Good morning. my love KIM."`

* `lower`

  * **모든 문자**를 **소문자**로 변경
  * `str = str.lower()`
    * `"good morning. my love kim."`

* `upper`

  * **모든 문자**를 **대문자**로 변경
  * `str = str.upper()`
    * `"GOOD MORNING. MY LOVE KIM."`

* `swapcase`

  * **소문자는 대문자**로, **대문자는 소문자**로 변경
  * `str = str.swapcase()`
    * `"gOOD MORNING. MY LOVE kim."`

* `capitalize`

  * 문자열의 **맨 앞 문자**만 **대문자**로 변경
  * `str = str.capitalize()`
    * `"Good morning. my love kim."`

* `title`

  * 문자열의 **한 단어마다의 맨 앞 문자**를 **대문자**로 변경

  * `str = str.title()`

    * `"Good Morning. My Love Kim."`

      

#### [공백 제거]

* `lstrip`
  * 왼쪽 공백 제거
* `rstrip`
  * 오른쪽 공백 제거
* `strip`
  * 좌우 공백 제거



### (4) 분할

> `str = "짬뽕 짜장 탕슉"`

* `split`
  * `str.split(구분자)`
  * 구분자를 기준으로 문자열을 분할
  * 분할한 것을 변수에 대입하거나 출력해보면, `리스트`가 되어있지!
  * 구분자가 공백일 경우, 공백`" "`이 구분자
  * `str.split()`
    * ` ['짬뽕', '짜장', '탕슉']`
* `splitlines`
  * 개행 문자나 파일 구분자 등 기중느로 문자열 잘라 리스트로 만듬



### (5) 끼워 넣기

* `join`

  * 문자열의 각 문자 사이에 다른 문자열을 끼워넣음

  ```python
  str = "._."
  print(str.join("대한민국")) # "대._.한._.민._.국"
  ```

  

### (6) 대체

* `replace`
  * 특정 문자열을 찾아 다른 문자열로 대체 (**모두 찾아냄**)
  * `str.replace(검색할 문자열, 바꿀 문자열)`



### (7) 정렬

* `just`
  * 문자열을 특정 폭에 맞추어 정렬
  * `str.ljust(30)`, `str.rjust(30)`
* `center`
  * 중앙 정렬
  * `str.center(30)`



### (8) 문자열로 구성된 리스트를 하나의 문자열로 만들어주기

* `[연결문자].join(리스트)`

* 예시

  ```python
  colors = ['red', 'blue', 'green', 'yellow']
  result = ''.join(colors)    # redbluegreenyellow
  result = ','.join(colors)    # red,blue,green,yellow
  ```

  

---



## 포맷팅

>  문자열 사이사이에 다른 정보 삽입하여 조립하는 방법

* 여러가지 포맷팅 방법

```python
stname = "김"
stage=26
stavg=90,123

# string cat
print(stname, "학생은 나이가", stage, "이고 평균은", stavg, "입니다")
print(stname+"학생은 나이가"+str(stage)+"이고 평균은"+str(stavg)+"입니다")
str1 = stname+"학생은 나이가"+str(stage)+"이고 평균은"+str(stavg)+"입니다"

# format % value
print("%s학생은 나이가 %d이고 평균은 %.2f입니다" %(stname, stage, stavg))
str2 = "%s학생은 나이가 %d이고 평균은 %.2f입니다" %(stname, stage, stavg)

# '{}'.format()
print("{}학생은 나이가 {}이고 평균은 {:2f}입니다".format(stname, stage, stavg))
str3 = "{}학생은 나이가 {}이고 평균은 {:2f}입니다".format(stname, stage, stavg)

# f-Strings
print(f"{stname}학생은 나이가 {stage}이고 평균은 {stavg:.2f}입니다")
str4 = f"{stname}학생은 나이가 {stage}이고 평균은 {stavg:.2f}입니다"
```



### (1) `format % values`

> 요즘 잘 안씀

* `%[-][폭][.유효자리수]서식`

* * `%`
  * `-`
    * `-`를 지정하면 **왼쪽 정렬**
    * 생략하면, `폭`에 기반하여 **오른쪽 정렬**
  * `폭`
    * 생략하면, 변수 크기만큼 준비하여 출력
  * `.유효자리수`
    * 소수점 아래 표시 자리수 설정
    * 생략하면, `6자리`
  * 서식
    * `d(정수), f(실수), s(문자열), c(문자 하나), h(16진수), o(8진수), %(% 문자)`

* 1000단위 마다 `,` 사용하기

  ```python
  num = 1000000
  print("%s" % format(num, ','))    # 1,000,000
  ```



### (2)`'{}'.format()` (3.0 버전부터)

> 3.0 버전부터

* `{ 인덱스 : [공백채울문자][정렬][폭][.유효자리수]서식 }`

  * 인덱스는 생략 가능
  * 대부분의 설명은 `format % values` 와 동일
  * `공백채울문자`
    * 폭과 정렬로 인해 만들어진 공백대신 채울 문자
    * 디폴트는 공백
    * 0으로 채우려면, `[정렬]0`과 같이 정렬 다음에 0을 적어야 함.

  * `정렬`
    * `^` : 가운데 정렬, `>` : 오른쪽 정렬, `<` : 왼쪽 정렬
    * 디폴트는 오른쪽 정렬

* 1000 단위마다 `,` 사용하기

  ```python
  num = 1000000
  print('{:,}'.format(num))
  ```

  

### (3) `f-Strings`

> 3.6 버전부터 
>
> 효능 좋음. 권장.

* `f "{변수명:[공백채울문자][정렬][폭][.유효자리수]서식}"`

  * **`f`를 꼭 지정해줘야 `f-Strings` 사용 가능!!!**

* 대부분의 설명은 `'{}'.format()` 와 동일

* 1000 단위마다 `,` 사용하기

  ```python
  num = 1000000
  print(f'{num:,}')
  ```

  
