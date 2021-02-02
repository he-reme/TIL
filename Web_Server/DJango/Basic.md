# Django

>  파이썬으로 작성된 오픈 소스 웹 애플리케이션 프레임워크
>
> `모델-뷰-컨트롤러 패턴`을 따르고 있음

#### 환경

* python 3.8.7
* pycharm

#### 목차

* 라이브러리와 프레임워크
* MVC 패턴
* MTV 패턴
* 장고의 처리 흐름
* 가상환경 만들기
* 장고 개발 환경 설치하기
* 장고 프로젝트 만들기
* Pycharm에서 사용을 위한 환경 설정



---



## 라이브러리와 프레임워크

### 라이브러리(API)

* 재사용이 필요한 기능으로 반복적인 코드 작성을 없애기 위해 언제든지 필요한 곳에서 호출하여 사용할 수 있도록 `Class`나 `Function`으로 만들어진 것

### 프레임워크

* 원하는 기능 구현에만 집중하여 빠르게 개발 할 수 있도록 기본적으로 필요한 기능을 갖추고 있는 것

* 라이브러리가 포함됨



---



## MVC 패턴

> Model View Controller 패턴

* 장고 프로그래밍에서 사용되는 개발 패턴
* SW 개발 패턴
* 이 패턴을 성공적으로 사용하면
  * 사용자 인터페이스로부터 비즈니스 로직을 분리하여 
  * 애플리케이션의 시각적인 요소나 
  * 그 이면에서 실행되는 비즈니스 로직을 
  * 서로 영향없이 쉽게 유지보수할 수 있는 애플리케이션을 만들 수 있음



### Model

* 애플리케이션에서 처리하는 데이터

### View

* 사용자 인터페이스 요소

### Controller

* 데이터와 비즈니스 로직 사이의 상호동작을 관리

### MVC 패턴 기반의 웹

* 요청 로직은 `Controller`로
* 응답 로직은 `View`로
* 처리 데이터는 `Model`로 

개발하여 확장성과 유지보수를 향상시킬 수 있게 됨.



---



## MTV 패턴

> 장고 프레임워크에서의 MVC 패턴

### Model

* MVC 패턴의 `Model`
* 데이터 관리 (DB 동작)
* 데이터베이스에 저장되는 데이터 영역

### Template

* MVC 패턴의 `View`
* 사용자가 보는 화면 (인터페이스)
* 사용자에게 보여지는 영역

### View

* MVC 패턴의 `Controller`
* 중간 관리자 (상호작용)
* 실질적으로 프로그램 로직이 동작하여 적절한 처리 결과를 `Template`에게 전달하는 역할



---



## 장고의 처리 흐름

> 웹 클라이언트의 요청을 받아 장고에서 MTV 모델에 따라 처리하는 과정

1. **클라이언트로부터 요청**을 받으면 `URL conf` 모듈을 이용하여 **URL을 분석**
2. URL 분석 결과를 통해 해당 **URL에 매칭되는 뷰를 실행**
3. **뷰는 자신의 로직을 실행**하고, **데이터베이스 처리가 필요하면 모델을 통해 처리**하고 그 결과를 반환 받음
4. **뷰**는 자신의 로직 처리가 끝나면 **템플릿을 사용하여 클라이언트에 전송할 HTML 파일을 생성**
5. **뷰**는 **최종 결과로 HTML 파일을 클라이언트에게 보내 응답함**



---



## 가상환경 만들기

> (2)번부터 cmd에 입력

#### (1) 가상환경을 위한 폴더 생성

`c:/KHR/python_venv` 폴더 생성

#### (2) 해당 폴더로 이동

`cd c:/KHR/python_venv`

#### (3) 가상환경 `djangovenv` 생성

`python -m venv djangovenv`

#### (4) 생성된 `djangovenv` 폴더의 `Scripts` 폴더로 이동

`cd djangovenv\Scripts`

#### (5) `activate` 프로그램을 실행하여, 가상환경 활성화

`activate`

* 가상환경을 활성화하면 명령 프롬프트 맨 앞에 `(djangovenv)` 가 붙은 것을 확인할 수 있음.
* `(djangovenv) C:\KHR\python_venv\djangovenv\Scripts>`



---



## 장고 개발 환경 설치하기

> 위에서 만든 가상환경 안에 설치
>
> 가상환경을 활성화한 상태에서 진행

#### (1) 가상환경 안에 장고 개발 환경을 설치하기 위해 pip 명령 실행 (장고 라이브러리 설치)

`pip install django`

#### (2) 시스템에 설치된 pip 버전 관련 경고 오류가 출력되면, 다음 명령을 실행시켜 업그레이드 진행

`python -m pip install --upgrade pip`



---



## 장고 프로젝트 만들기

#### (1) 폴더 생성

`c:/KHR/DJANGOexam` 폴더 생성

#### (2) 해당 폴더로 이동

`cd c:/KHR/DJANGOexam`

#### (3) 장고 프로젝트 생성 

`django-admin startproject [프로젝트명]`

* 학습용으로 만든 내 프로젝트명: `studyproject`

#### (4) 생성된 폴더로 이동

`cd studyproject`

#### (5) 장고에 내장된 서버 가동시키기

`python manage.py runserver`

* `ctrl+c` : 서버 종료

#### (6) 크롬 브라우저에서 `http://localhost:8000/` 입력하여 요청

* 기본 웹 페이지가 출력되는 것을 확인할 수 있음



---



## Pycharm에서 사용을 위한 환경 설정

> 자세한 그림과 설명은 문서 확인

#### (1) 위에서 만든 프로젝트를 오픈 Pycharm에서 오픈

* `File > Open`을 선택

* `c:\KHR\DJANGOexam\studyproject` 오픈

#### (2) 프로젝트 인터프리터 설정 : 가상환경으로 선택

* `File > Setting`을 선택
* `Project: studyproject` 탭의 `Python Interpreter` 를 선택
* `톱니바퀴 > Add` 선택
* `Existing environment` 체크
* `...` 버튼 클릭
* `C:\KHR\python_venv\djangovenv\Scripts\python.exe` 선택
* `OK` 버튼 계속 클릭~~ 끝~~



---



## 프로젝트 세팅

> 처음 시작 시

#### (1) `settings.py` 수정

`C:\KHR\DJANGOexam\studyproject\studyproject\settings.py`

* **106줄** - 한국어 설정 

  `LANGUAGE_CODE = 'ko-kr'`

*  **108줄** - 한국 시간으로 설정

  `TIME_ZONE = 'Asia/Seoul'`