# 함수



## 인수

### (1) 가변 인수

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



### (2) 가변 키워드 인수

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



## 일급객체

> 파이썬의 함수는 일급객체!
>
> 일급객체
>
> : 다른 객체들에 일반적으로 적용 가능한 연산을 보두 지원하는 객체
>
> : 보통 함수에 매개변수로 넘기기, 수정하기, 변수에 대입하기와 같은 연산을 지원할 때 일급객체라고 함.



### 파이썬의 함수

* 변수에 저장할 수 있으며, 함수를 담고있는 변수를 통해 함수를 호출할 수 있다.

  ```python
  def func() :
      print("func 호출 - hello")
      
  v = func
  print(func)    # <function func at 0x0000020174B76670>
  print(v)    # <function func at 0x0000020174B76670>
  v()    # func 호출 - hello
  ```

* 다른 함수 호출 시 인수로 전달 가능하다.

  ```python
  import types
  
  def say() :
      print("안녕?")
  
  def func(fn) :
      if type(fn) == types.FunctionType :    # 함수를 인수로 받았으면
          fn()
      else :
          print("인수로 함수를 주세요")
  
  func(say)    # 안녕?
  callback(100)    # 인수로 함수를 주세요
  ```

* 함수의 리턴 값으로 전달 가능하다.

  ```python
  def fct_fac(n) :
      def exp(x) :
          return x**n
      return exp
  
  func = fct_fac(2)
  
  print(type(func))    # <class 'function'>
  print(func(4))    # 16
  ```

* 일반적인 데이터처럼 사용 가능하다.



---



## 컬렉션 관리 함수

### (1) `enumerate`

* 순서값과 요소값을 한꺼번에 구하는 내장함수

* 예시1

  ```python
  score = [ 88, 95, 70, 100, 99 ]
  for no, s in enumerate(score, 1):
      print(str(no) + "번 학생의 성적 :", s)
  '''
  1번 학생의 성적 : 88
  2번 학생의 성적 : 95
  3번 학생의 성적 : 70
  4번 학생의 성적 : 100
  5번 학생의 성적 : 99
  '''
  ```

* 예시2

  ```python
  for i, v in enumerate(['tic', 'tac', 'toe']):
  	print(i,v)
  '''
  0 tic
  1 tac
  2 toe
  '''
  ```

  

### (2) `zip`

> **1회성!!** 

* 여러 개 컬렉션 합쳐 하나로 만듦
* 두 리스트의 대응되는 요소끼리 짝지어 **튜플 zip 객체** 생성

* zip 객체로 만들어준 후 `list()`, `dict()` 등의 함수를 통해 압축 해제(?) ㅎㅎㅎ 해줘야 함. 

  * 대신 압축 해제 했다고 해서 리스트나 딕셔너리가 되는 것은 아님. 
  * 출력해보면 `<zip object at 0x0000020804944280>` 이런식으로 출력 됨.
  * 1회성이기 때문에 한번 `list()`, `dict()` 등의 함수를 사용하면 값이 `[]`, `{}` 이런 식으로 비어서 나옴

* 예시1

  ```python
  yoil = ["월", "화", "수", "목","금", "토", "일"]
  food = ["갈비탕", "순대국", "칼국수", "삼겹살"]
  menu = zip(yoil, food)
  for y, f in menu:
      print("%s요일 메뉴 : %s" % (y, f))
  ''' 
  # 인덱스 대응되는 요소끼리..
  월요일 메뉴 ; 갈비탕
  화요일 메뉴 : 순대국
  수요일 메뉴 : 칼국수
  목요일 메뉴 : 삼겹살
  '''
  ```

* 예시2

  ```python
  zip1 = zip([1, 2, 3], [4, 5, 6])
  zip2 = zip([1, 2, 3], [4, 5, 6], [7, 8, 9])
  zip3 = zip("abc", "def")
  
  print(zip3)
  print(dict(zip1))
  print(list(zip2))
  print(dict(zip3))
  
  # 여기 아래 print 해보면 빈 객체가 출력됨. zip은 1회성이니까!
  # print(list(zip1))    []
  # print(list(zip2))    []
  # print(dict(zip3))    {}
  '''
  <zip object at 0x0000022020DB4200>
  {1: 4, 2: 5, 3: 6}
  [(1, 4, 7), (2, 5, 8), (3, 6, 9)]
  {'a': 'd', 'b': 'e', 'c': 'f'}
  '''
  ```

* 예시3

  ```python
  alist = ['a1', 'a2', 'a3']
  blist = ['b1', 'b2', 'b3']
  for a, b in zip(alist, blist):    # 병렬로 값을 추출
  	print(a, b)
  '''
  a1 b1
  a2 b2
  a3 b3
  ```

  

---



## 람다 함수

### (1) `filter`

* `filter(조건을 지정하는 함수, 대상 리스트)`

  * 조건을 지정하는 함수는 반드시 **bool형을 리턴하는 함수**여야 함

* 리스트 요소 중 조건에 맞는 것만을 골라냄

* 예시

  ```python
  def flunk(s):
  	return s<60
  	
  score = [45, 89, 72, 53, 94]
  for s in filter(flunk, score):
  	print(s)
  
  # 45
  # 53
  ```

  

### (2) `map`

* `map(값을 변환하는 함수, 대상 리스트)`
* 모든 요소에 대한 변환함수 호출, 새 요소 값으로 구성된 리스트 생성

* 예시

  ```python
  def half(s):
  	return s/2
  	
  score = [45, 89, 72, 53, 94]
  for s in map(half, score):
  	print(s, end=', ')
  	
  # 22.5, 44.5, 36,0, 26.5, 47.0,
  ```

  

### (3) `lambda`

* `lambda 인수:식`
  * **인수** : 호출 시 전달받을 아규먼트 (생략 가능), 여러 개 가질 수 있음
  * **식** : 하나만 올 수 있음

* **이름 없고 입력과 출력만으로 함수를 정의**하는 축약된 방법

* 예시1

  ```python
  a = lambda :100
  b = lambda x:x*1000
  c = lambda v1,v2:v1+v2
  d = lambda v1,v2:v1>v2
  e = lambda v1,v2,v3:sum([v1,v2,v3])
  
  a()    # 100
  b(3)    # 3000
  c(10, 20)    # 30
  d(5, 3)    # True
  e(10, 20, 30)    #60
  ```

* 예시2

  ```
  score = [45, 89, 72, 53, 94]
  for s in filter(lambda x:x < 60, score):
  	print(s)
  ```

  