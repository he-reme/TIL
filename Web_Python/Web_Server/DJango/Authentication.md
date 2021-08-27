# 인증 시스템

> 로그인 기능과 로그아웃 기능

* Django에는 **로그인 기능과 로그아웃 기능**을 지원하는 **앱과 미들웨어 프로그램을 내장**

  ```python
  # 장고프로젝트/settings.py
  INSTALLED_APPS = [
  	... ,
  	'django.contrib.auth',
  	... ,
  ]
  
  MIDDLEWARE = [
      ... ,
      'django.contrib.auth.middleware.AuthenticationMiddleware',
      ... ,
  ]
  ```



---



## 회원 정보 저장 DB

> 내장된 앱과 미들웨어 프로그램에 의해서 관련된 DB 테이블들이 최초로 수행된 migrate 명령에 의해 생성됨

* `django.contrib.auth` 앱에서 제공되는 `User`라는 모델 클래스를 통해,
* 회원을 가입하고 가입된 회원 정보를 통해서 로그인과 로그아웃 기능을 간단하게 처리할 수 있음
* 해당 모델 클래스는 HeidSQL 에서 `auth_user` 테이블에 해당

* 실습에서는 해당 테이블의 속성 네개만 저장할 것임
  * `username` 
    * 아이디
    * `email` 컬럼 사용 안하고 `username`을 그냥 이메일로 받을 예정
  * `password` 
  * `last_name`
  * `first_name`



---



## 관련 API

```
from django.contrib import auth
from django.contrib.auth.models import User
```

#### (1) 회원가입

```
User.objects.create_user(회원정보를 키워드 아규먼트로 설정)
```

* 예시

  ```
  user = User.objects.create(
  	username = useremail,
  	first_name = firstname,
  	last_name = lastname,
  	password = password
  )
  ```

#### (2) 회원인지 체크

```python
auth.authenticate(username=사용자계정, password=사용자패스워드)
```

* 리턴값
  * 회원이 아니면, `None`
  * 회원이면, `해당 회원의 User 객체`

#### (3) 로그인

```python
auth.login(request, User객체)
```

#### (4) 로그인 여부 체크

```python
request.user.is_authenticated
```

#### (5) 로그아웃

```python
auth.logout(request)
```

