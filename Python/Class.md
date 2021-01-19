# Class

> 객체지향의 가장 기본적 개념
>
> **관련된 속성과 동작을 하나의 범주로 묶어 실세계의 사물을 흉내** 냄

* 모델링 : 사물을 분석하여 필요한 속성과 동작을 추출하는 것
* 캡슐화 : 모델링한 결과를 클래스로 포장하는 것



---



## 기본

### (1) 클래스 정의 방법

```python
class 클래스명:
	변수 정의
	변수 정의
	함수 정의
	함수 정의
```



### (2) 객체 생성 방법

```python
변수 = 클래스명()
```



### (3) 객체 사용 방법

```python
변수.변수명
변수.메서드명()
```



### (4) 객체 생성과 삭제

```python
class 클래스명:
	def __init__(self):    # 생성 시 자동 호출
		print("객체 생성")
	def __del__(self):    # 삭제 시 자동 호출
		print("객체 삭제")
```

* `del`
  * 프로그램이 종료되면 자동으로  호출됨
  * 강제 삭제하고 싶으면: `del 객체명`
  * `init`과 다르게 생략하는 경우 많음



---



## 생성자

> 초기화 메소드

* `__init__ 생성자` 

  ```python
  class 이름:
  	def __init__(self, 초기값):
  		멤버 초기화
  ```

  * 주로 변수 초기화 하는 데 사용
  * `self` : 해당 객체 `자기 자신`을 가리킴

* 예시

  ```python
  lass student:
  	def __init(self, name, age, subject):
  		self.name = name
  		self.age = age
  		self.subject = subject
  	
  	def printInfo(self):
  		print(self.name, self.age, self.subject)    # self 꼭 붙여줘야 함
  		
  st = student("혜림", 25, 빅데이터)
  st.printInfo()
  print(st.name, st.age, st.subject)
  ```

  

---



## 상속

> 기존 클래스를 확장하여 멤버를 추가하거나 동작을 변경

```python
class 클래스명(부모클래스명):
	...
```

* `super().함수`
  * 부모의 함수를 호출하고 싶을 때 사용



---



## 클래스 변수

> **해당 클래스로 만들어진 인스턴스 모두** 접근할 수 있는 변수
>
> 해당 인스턴스들이 공유했으면 하는 변수에 사용

```python
class 클래스명:
    count = 0    # 클래스 변수
    def __init__(self, name, age):
        # 인스턴스 변수 초기화
        self.name = name
        self.age = age
```

* 접근 방법 : `클래스명.클래스변수`



#### 클래스 변수 VS 인스턴스 변수

* 클래스 변수 
  * **`init` 함수 밖**에서 초기화한 변수
  * 같은 클래스로 생성된 모든 인스턴스가 **공유**하는 변수

* 인스턴스 변수 
  * **`init` 함수 안**에서 초기화한 변수
  * 인스턴스 **개별**로 사용하는 변수

