# Python

## cmd

### (1) `python` 

인터렉티브 모드 실행



### (2) `python [이름.py]`

파이썬 소스코드 실행



---



## 기본

### (1) 주석 

* 단일행 주석 : `#` 주석입니다

* 다중행 주석 : `"""` 주석입니다

  ​							 주석입니다

  ​							 주석입니다 `"""`



### (2) 출력

* `print` 명령
  * `print(출력내용, [, sep=구분자][, end=끝 문자])`
  * `sep`의 default : 공백



### (3) 입력

* `input` 명령

  * 사용자에게 질문하여 값 입력받기
  *  `변수 = input('질문내용')`
  * 사용자가 질문에 대한 입력한 값을 돌려받아 변수에 대입
  * 그냥 `input` 명령을 사용하게 되면 `문자열`로 입력됨

  

---



## 변수

### (1) 변수명

* 변수
  * 메모리에 이름 붙이고 값을 저장하는 것
* 명칭
  * 변수가 다른 것과 구분되도록 이름을 붙인 것
* 변수명 규칙
  * 예약어 사용 불가
  * 숫자 시작 불가
  * 특수문자는 _(언더스코어)만 사용 가능
  * 공백 사용 불가
  * 대소문자 구분



### (2) 변수 사용

* 파이썬 변수는 타입을 지정하지 않음
* 대입하는 값에 의해 결정
* 동적타입 (Dynamic Type)
  * 실행 중에 변수 타입 바꿀 수 있음
  * 현재 할당하고 있는 값에 의해 변수의 타입이 정해짐



---



## datetime 객체

> 날짜 관련

* `import datetime`

* 사용 예시)

  ```python
  import datetime
  now = datetime.date.today()
  print(now.weekday()) # 1
  print(now.ctime()) # Tue Jan 12 00:00:00 2021
  ```

  ```python
  import datetime
  christmas = datetime.date(2021, 12, 25)
  print(christmas.weekday()) # 5
  print(christmas.ctime()) # Sat Dec 25 00:00:00 2021
  ```

  * `weekday()` 
    * `0:월, 1:화, 2:수, 3:목, 4:금, 5:토, 6:일`



---



## 출력과 포맷팅

>  포맷팅 : 문자열 사이사이에 다른 정보 삽입하여 조립하는 방법

* 여러가지 방법

```python
stname = "김"
stage=26
stavg=90,123

# string cat
print(stname+"학생은 나이가"+str(stage)+"이고 평균은"+str(stavg)+"입니다")
print(stname, "학생은 나이가", stage, "이고 평균은", stavg, "입니다")

# format % value
print("%s학생은 나이가 %d이고 평균은 %.2f입니다" %(stname, stage, stavg))

# '{}'.format()
print("{}학생은 나이가 {}이고 평균은 {:2f}입니다".format(stname, stage, stavg))

# f-Strings
print(f"{stname}학생은 나이가 {stage}이고 평균은 {stavg:.2f}입니다)
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



### (2)`'{}'.format()` (3.0 버전부터)

> 3.0 버전부터



### (3) `f-Strings`

> 3.6 버전부터 
>
> 효능 좋음. 권장.



---



## 함수

### (1) 가변 아규먼트

* 매개변수명 앞에 `*`를 붙여서 사용

* `p`는 튜플 형태

  ```python
  def testFunc(*p):
      list = []
      for i in p:
          list.append(i)
      return list
      
  print(testFunc(2, 1, 2, 3, 4, 5))    #[2, 1, 2, 3, 4, 5]
  ```



### (2) 가변 키워드 아규먼트

* 매개변수명 앞에 `**`를 붙여서 사용

* `키=값` 형태로 인자 전달

* `kargs`는 딕셔너리 형태

  ```python
  def testFunc(a, **kargs) :
  	print(kargs)    # {'b':2, 'c'=3, 'd'=4, 'e'=5, 'f'=6}
      for key, value in kargs.items() :
          print(key, value)
  
  testFunc(1, b=2, c=3, d=4, e=5, f=6)    # 'b'=2 처럼 키를 문자열로 쓰면 에러
  ```




---



## 패킹

> 변수 앞에 `*`를 붙이는 것



* 요소 단위로 넘김

* 예시1

  ```python
  list = [1, 2, 3, 4, 5]
  print(*list)    # 1 2 3 4 5 로 출력됨 
  				# = print(list[0], list[1], list[2], list[3], list[4])
  ```

* 예시2

  ```
  x, *y, z = [10, 20, 30, 40]
  print(x)    # 10
  print(y)    # [20, 30]
  print(z)    # 40
  ```

  