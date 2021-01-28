# Django

> 파이썬으로 작성된 오픈 소스 웹 애플리케이션 프레임워크
>
> `모델-뷰-컨트롤러 패턴`을 따르고 있음

* 환경
  * python 3.8.7
  * pycharm



---



## 장고의 처리 흐름

> 웹 클라이언트의 요청을 받아 장고에서 MTV 모델에 따라 처리하는 과정

1. **클라이언트로부터 요청**을 받으면 `URL conf` 모듈을 이용하여 **URL을 분석**
2. URL 분석 결과를 통해 해당 **URL에 매칭되는 뷰를 실행**
3. **뷰는 자신의 로직을 실행**하고, **데이터베이스 처리가 필요하면 모델을 통해 처리**하고 그 결과를 반환 받음
4. **뷰**는 자신의 로직 처리가 끝나면 **템플릿을 사용하여 클라이언트에 전송할 HTML 파일을 생성**
5. **뷰**는 **최종 결과로 HTML 파일을 클라이언트에게 보내 응답함**



---



## 장고 프로젝트 폴더

#### templates

* html 파일들 보관

#### static

* 정적 파일 보관



---



## 장고를 이용한 웹 서버 프로그래밍

#### `urls.py`

* 프로젝트 폴더(메인)와 앱폴더(서브)
* 요청 시 사용될 `URL` 문자열의 `path`와 호출될 `뷰의 함수`를 결정
  * `라우팅을 정한다`라고도 함

#### `views.py`

* 앱 폴더
* `GET` 방식 요청을 처리할 것인지, `POST` 방식 요청을 처리할 것인지 결정하고
* 요청에 대한 기능을 수행하도록 `urls.py`에서 설정한 함수에 로직을 구현

#### `templates/xxx.html`

* 수행한 결과를 클라이언트로 응답하는 기능의 템플릿을 구현



---



## Pycharm Terminal 사용

#### 서버 가동

`python manage.py runserver`

#### 장고 앱 (서버 앱) 생성

`python manage py startapp 장고앱명`

* 장고앱 생성할 때마다 `C:\KHR\DJANGOexam\studyproject\studyproject\setting.py` 

  의 `INSTALLED_APPS`에 추가해줘야 한다. 



---



## HttpRequest / HttpResponse

> 장고는 `request`와 `response` 객체로 서버와 클라이언트가 정보를 주고 받는다.
>
> 이를 위해 장고는 `django.http` 모듈에서 `HttpRequest`와 `HttpResponse` API를 제공한다.

#### 서버-클라이언트 통신 시 절차로 데이터가 오고감

1. 특정 페이지가 요청(request)되면, 장고는 메타데이터(여러 다양한 정보)를 포함하는 `HttpRequest` 객체 생성
2. 장고는 `urls.py`에서 정의한 특정 `View`함수에 첫 번째 인자로 해당 객체(`HttpRequest`)를 전달
3. 해당 `View`는 결과값을 `HttpResponse` 혹은 `JsonResponse` 객체에 담아 전달



## HttpRequest 객체

> 주로 `request` 를 변수명으로 사용

* 요청 처리
* HTTP 프로토콜 기반으로 요청이 왔을 때 요청 관련 정보를 제공하는 객체
* 뷰함수가 호출될 때 인자로 전달됨
  * 장고 서버가 객체를 생성함

#### (1) 주요 속성

* `HttpRequest.body`

  * `request`의 `body` 객체

* `HttpRequest.headers`

  * `request`의 `headers` 객체

* `HttpRequest.COOKIES`

  * 모든 쿠키를 담고 있는 딕셔너리 객체

* `HttpRequest.method`

  * `request`의 메소드 타입 반환
  * 메소드 타입 : `GET`, `POST`

* `HttpRequest.GET`

  * `GET` 파라미터를 담고 있는 딕셔너리 같은 객체

  * `변수 = HttpRequest객체.GET.get('키', 'default값')`

    * GET 방식으로 요청받은 쿼리문에서 `키`를 찾아 값을 얻고,
    * 해당 키에 값이 없으면 `default값`을 얻어
    * 얻은 값을 변수에 대입함
    * 여러개인 경우 `getlist` 사용!
      * `변수 = HttpRequest객체.GET.getlist('키', 'default값')`

  * `변수 = HttpRequest객체.GET['키']`

    * `default값` 지정할 수 없음
    * 값이 없으면 에러뜨나?

  * 사용 예시

    `name = request.GET.get('name', '게스트')`

    `name = request.GET.get['name']`

* `HttpRequest.POST`

  * `POST` 파라미터를 담고 있는 딕셔너리 같은 객체

  * `변수 = request.POST.get('키', 'default값')`

    * POST 방식으로 요청받은 쿼리문에서 `키`를 찾아 값을 얻고,
    * 해당 키에 값이 없으면 `default값`을 얻어
    * 얻은 값을 변수에 대입함
    * 여러개인 경우 `getlist` 사용!
      * `변수 = HttpRequest객체.POST.getlist('키', 'default값')`

  * `변수 = int(request.POST['키'])`
    
    * `default값` 지정할 수 없음
    
  * 사용 예시

    `name = request.POST.get('name', '게스트')`

    `name = request.POST.get['name']`

* `HttpRequest.GET`, `HttpRequest.POST` 예시

  * `HttpRequest.GET`, `HttpRequest.POST` 은 문자열로 반환되기 때문에
  * 원하는 데이터 타입이 있으면 변환해줘야 함

  ```python
  def exam2_1(request) :
      if request.method == 'GET' :
         msg = request.GET.get("info1", "없음") + "-" + request.GET.get("info2", "없음") + "-" + request.GET.get("info3", "없음")
      else :
         msg = request.POST.get("info1", "없음")  + "-" + request.POST.get("info2", "없음")  + "-" + request.POST.get("info3", "없음")
      context = {'result' : msg}
      return render(request, 'exam2_1.html', context)
  ```


#### (2) 주요 메소드

* `HttpRequest.read`

* `HttpRequest.get_host()`

* `HttpRequest.get_port()`

  

## `HttpResponse` 객체

* 응답 처리

* HTTP 프로토콜 기반으로 온 요청에 대한 응답시 사용하는 객체
* 응답 내용을 담게 됨
  * 인자 : HTML 태그 문자열, 탬플릿을 사용한 랜더 객체

#### (1) `HttpResponse(data, content_type)`

* `response`를 반환하는 가장 기본적인 함수
* 주로 `html`를 반환

#### (2) `string` 전달하기

```python
HttpResponse("원하는 문자열")
```

#### (3) `html 태그` 전달하기

```python
response = HttpResponse()
response.write("<태그>원하는 문자열</태그>")
```



## 요청 방식

> URL을 요청할 때 맨 마지막에 `/`붙여줘야 함!

### GET

* `직접 URL을 입력`하여 요청했을 때
* `<a>` 태그로 요청했을 때
* `<form>` 태그로 `GET` 방식으로 요청했을 때
* `<img>` 태그로 요청했을 때

### POST

> 보안에 좋음

* `<form>` 태그로 `POST` 방식으로 요청했을 때 
* URL을 요청할
* `POST` 방식은 엄격하기 때문에 `/`가 맨 마지막에 붙여지지 않은 URL을 요청하면 `500 error`를 발생시킴



---



## HttpRedirect

#### `HttpResponseRedirect(url)`

* 별다른 `response`를 하지는 않고, 지정된 url 페이지로 `redirect`함
* 첫번째 인자는 반드시 `url`로 지정
* 경로는 절대경로/상대경로 이용 가능



## Render

> `render`는 `httpResponse` 객체를 반환하는 함수로
>
> `template`를 `context`와 엮어 `HttpResponse`로 쉽게 반환해 주는 함수

`render(request(필수), template_name(필수), content=None, content_type=None, status=None, using=None)`

* `context`에는 `View`에서 사용하던 변수(dictionary 자료형)을 `html` 템플릿에 전달하는 역할
  * `key`값 : 템플릿에서 사용할 변수 이름
  * `value값` : 파이썬 변수 값

* `HttpResponse 객체` 반환 코드를 간단하게 만들어줌.

```python
from django.shortcuts import render // 랜더를 간단하게!
return render(request객체, 템플릿파일(html), 딕셔너리객체(context))
```

* 예시

  * 아래의 코드를

    ```python
    template = loader.get_template('exam2_1.html')
    return HttpResponse(template.render(context, request))
    ```

  * 아래의 코드로 만들 수 있음

    ```python
    return render(request, 'exam2_1.html', context)
    ```



## JsonResponse

> `HttpResponse`의 `subclass`로, 
>
> `JSON-encoded response`를 생성할 수 있게 해 줌

`JsonResponse(data, encoder=DjangoJSONEncoder, safe=True, json_dumps_params=None, **kwargs)`

* 대부분의 기능은 `superclass`에서 상속받음
* 첫 번째 인자 : 전달할 데이터로서 반드시 `dictionary` 객체여야 함
* 디폴트 `Content-type 헤더` : `application/json` 임
* `encoder` : 데이터를 `serialize`할 때 이용
* `jason_dumps_params` : `json.dumps()`에 전달할 딕셔너리의 `keyword arguments`임

#### `Serializing non-dictionary objects`

`response = JsonResponse([1, 2, 3], safe=False)`



---



## Query 문자열

> HTTP Client 가 HTTP Servr에 요청시 서버에서 요청하려는 대상의 URI이 전달되는데 이 때 함께 전달될 수 있는 문자열

* `name=value` 형식으로 구성되어야 한다.
* 여러개의 `name=value`가 사용될 때는 `&` 기호로 구분되게 구성해야 한다.
* 영문과 숫자는 그대로 전달되지만, 한글과 특수문자들은 `%` 기호와 16진수 코드값으로 전달된다. (UTF-8)
* 공백문자는 `+` 기호 또는 `%2C`로 전달된다.
* Query 문자열을 가지고 **HTTP Server에게 정보를 요청할 때는 2가지 요청 방식** 중 한개 선택할 수 있다.

* 예시

  `http://localhost:8000/secondapp/exam2_1/?info1=hereme&info2=hello&info3=world`

#### `GET` 방식으로 요청할 경우

* Query 문자열이 외부에 보여짐 (URL에 보임)
  * 요청 URL 뒤에 `?` 기호와 함께 전달되기 때문
* 외부에 보여줘도 관계 없을 경우 사용

#### `POST` 방식으로 요청할 경우

* Qyery 문자열이 외부에 보여지지 않음 (URL에 보이지 않음)
* 외부에 보여지면 안될 경우 사용



---



## Django 템플릿

>  HTML 파일에서 사용
>
>  템플릿을 만들다 = HTML을 만들다
>
>  4가지 기능 제공 : 변수, 필터, 태그, 주석

### 템플릿 변수

##### `{{ 변수명 }}`

* 값 표현
* 뷰함수가 반환한 딕셔너리의 **키**
  * 장고 템플릿 안에 있는 변수는 모두 뷰함수가 반환한 딕셔너리 키 사용
* 템플릿 변수를 사용하면 뷰에서 템플릿으로 객체 전달 가능
* 변수명으로 데이터 값 추출이 안되는 경우 : 공백으로 처리

### 템플릿 필터



### 템플릿 태그 (로직)

##### `{% 로직 %}`

* 로직 구현 
* if문, for문처럼 흐름 제어 가능

#### 1. csrf_token 

* 사이트 간 요청 위조(=크로스 사이트 요청 위조)를 해결하기 위한 처리
* `POST` 방식 `<form>` 태그 안에 꼭 작성

```html
{% csrf_token %}
```

#### 2. for

````html
{% for 변수명 in 시퀀스명 %}
{% endfor %}
````

#### 3. if / else

```html
{% if 조건문 %}
{% elif %}
{% else %}
{% endif %}
```

#### 4. block 및 extends

* 중복되는 html 파일 내용을 반복해서 작성해야 하는 번거로움을 줄여줌
* 템플릿 확장

```html
{% extends "html파일" %}
{% block title %}{{ section.title }}{% endblock %}
{% block content %}
{% endblock %}
```



### 템플릿 코멘트

* HTML 문서 상에서 주석이 필요할 때 사용
* 장고에서는 2가지 코멘트 형식을 제공

#### 한 줄

```html
{# 주석 내용 #}
```

#### 여러 줄

```html
{# comment #}
<!-- 주석 내용 -->
{# endcomment #}
```





---

 

## block 및 extends

> 중복되는 html 파일 내용을 반복해서 작성해야 하는 번거로움을 줄여줌
>
> 템플릿 확장

```html
{% extends "html파일" %}
{% block title %}{{ section.title }}{% endblock %}
{% block content %}
{% endblock %}
```

