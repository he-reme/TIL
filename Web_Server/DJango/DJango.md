# Django

> 파이썬으로 작성된 오픈 소스 웹 애플리케이션 프레임워크
>
> `모델-뷰-컨트롤러 패턴`을 따르고 있음

* 파이썬 : 3.8.7



---



## 가상환경 만들기

#### (1) 가상환경을 위한 폴더 생성

`c:/KHR/python_venv` 폴더 생성

> 아래부터는 cmd에 입력

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



## Pycharm에서 사용

> 문서 확인

