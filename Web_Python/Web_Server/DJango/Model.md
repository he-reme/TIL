# Django Model

> Django의 Model

* **데이터 서비스 제공**
* 각 Django App안에 기본적으로 생성되는 `models.py` 모듈 안에 정의

* Django가 사용하는 SQL

  * python이 내장하고 있는 SQLite

  

---



## CRUD

> Create : 데이터 생성
>
> Read : 데이터 읽기
>
> Update : 데이터 수정
>
> Delete :  데이터 삭제

* CRUD : Django를 통한 DataBase 연동

* SQL (INSERT, SELECT, UPDATE, DELETE)
* Django API (python)

#### CRUD 구현 과정

1. 모델 클래스를 생성
   * `models.py` 에 생성
   * `django.db.models.Model` 클래스를 상속해서 생성해야 함
   * 만들려는 DB 테이블의 컬럼 사양에 맞춰서 클래스 변수를 정의해야 함
2. Django에서 제공하는 명령을 수행시켜서 모델 클래스에 알맞는 DB테이블을 생성

3. 모델 클래스를 통해서 CRUD를 구현

   * C 

     * 모델 클래스의 객체를 생성한 후 `save()` 메서드 호출

   * R (SELECT)

     * `모델클래스.objects.all()`
     * `모델클래스.objects.filter(...)`
     * `모델클래스.objects.order_by(...)`
     * `모델클래스.objects.first()`
     * `모델클래스.objects.last()`
     * `모델클래스.objects.count()`

     

---



## model 클래스

> model은 클래스로 구현됨

* `models.py` 모듈 안에 하나 이상의 모델 클래스를 정의할 수 있음

* **하나의 모델 클래스**는 **데이터베이스에서 하나의 테이블**에 해당

* `django.db.models.Model`의 자식 클래스

#### model의 필드

* 클래스의 속성
* 테이블의 컬럼에 해당
* Primary Key(기본키)가 지정되지 않으면, 모델이 Primary Key 역할을 하는 id 필드가 자동으로 추가됨
  * id 필드 : 자동으로 값이 1씩 증가되는 id 컬럼
* Django에서 필드는 model을 생성할 때 필수적인 요소
* 필드명 주의 사항
  * clean, save, delete 등과 같은 model API와 동일한 이름으로 생성하지 않도록 주의



---



## model의 필드

#### model 클래스에 필드 정의

```
class 모델이름(models.Model):
	필드 이름1 = models.필드타입(필드옵션)
	필드 이름2 = models.필드타입(필드옵션)
```

* 인스턴스 변수가 아닌 **클래스 변수**로 정의

* 변수에는 테이블 컬럼의 메타 데이터를 정의

* 필드를 정의하는 각각의 클래스 변수는 각 필드 타입에 맞는 Field 클래스 객체를 생성하여 할당

  * `models.Charfield()`
  * `models.IntegerField()`
  * `models.DataTimeField()`
  * `models.TextField()`

  * Field 클래스는 여러 종류가 있는데, 생성자 함수 호출시 필요한 옵션들을 지정 가능

#### 필드 타입

> 모델의 필드에는 다음과 같이 다양한 타입들이 있음
>
> 모든 필드 타입 클래스들은 `Field` 클래스의 자손 클래스들임

* CharField

  * 제한된 문자열 필드 타입
  * 최대 길이를 max_length 옵션에 지정해야 함
  * CharField의 파생 클래스 (문자열의 특별한 용도에 따라)
    * EmailField : 이메일 주소 체크
    * GenericIPAddressField : IP 주소를 체크
    * CommaSeperatedIntegerField : 콤마로 정수를 분리
    * FilePathField : 특정 폴더의 파일  패스를 표현
    * URLField : URL을 표현

* TextField

  * 대용량 문자열을 갖는 필드

* IntegerField

  * 32비트 정수형 필드
  * 정수 사이즈에 따라 사용할 수 있는 다른 필드
    * BigIntegerField
    * SmallIntegerField

* BooleanFiled

  * true/false 필드
  * NullBooleanField : Null을 허용

* DateTimeField

  * 날짜와 시간을 갖는 필드
  * DateField : 날짜만 가질 경우
  * TimeField : 시간만 가질 경우
  * `auto_now_add(생성)`과  `auto_now(수정)`을 true로 설정하면, 생성 또는 수정시 기본 타임존 시간으로 변경됨

* DecimalField

  * 소숫점을 갖는 decimal 필드 

* BinaryField

  * 바이너리 데이터를 저장하는 필드

* FileField

  * 파일 업로드 필드

  * FileField의 파생 클래스
    * ImageField : 이미지 파일인지 체크

* 관계(Relation)를 표현하는 필드
  * ForeignKey
    * 모델 클래스간의 Many-To-One (혹은 One-To-Many) 관계를 표현하기 위해 흔히 사용됨
  * ManyToManyField
  * OneToOneField

#### 필드 옵션

> 모델의 필드는 필드 타입에 따라 여러 옵션 (혹은 Argument)를 가질 수 있음
>
> 예를들어, CharField는 max_length라는 옵션을 가짐
>
> 필드 옵션은 일반적으로 생성자에서 아규먼트로 지정함

**자주 사용되는 모든 필드 타입에 적용 가능 옵션**

* null
  * Field.null
  * `nul=True`이면, Empty 값을 DB에 NULL로 저장
  * DB 테이블에서 Null이 허용되는 필드가 됨
  * 예 : `models.IntegerField(null=True)`

* blank

  * Field.blank
  * `blank=False` 이면, Required 필드가 됨
  * `blank=True` 이면, Optional 필드가 됨
  * 예 : `models.DateTimeField(blank=True)`

* primary_key

  * Field.primary_key
  * 해당 필드가 Primary Key임을 표시
  * 모델 클래스에 Primary Key로 설정되는 필드가 없으면 id라는 필드가 자동 생성됨
  * 예 : `models.CharField(max_length=10, primary_key=True)`

* unique

  * Field.unique
  * 해당 필드가 테이블에서 Unique함을 표시함
  * 해당 컬럼에 대해 Unique Index를 생성
  * 예 : `models.IntegerField(unique=True)`

* default

  * Field.default
  * 필드의 디폴트값을 지정
  * 예 : `models.CharField(max_length=2, default="WA")`

  

---



## DB Migration

> **Migration** : Python 모델 클래스의 수정 및 생성을 DB에 적용하는 과정

* Django에서 Model 클래스를 생성하고 난 후, 
* 해당 모델에 상응하는 DB 테이블을 데이터베이스에서 생성할 수 있음
* Migration은 Django가 기본적으로 제공하는 ORM 서비스를 통해 진행됨

#### ORM

* O (Object) : 모델 클래스
* R (Relational) : 데이터베이스 테이블
* M (Mapping) : 모델 클래스와 데이터베이스 테이블을 매핑

#### 테이블 생성하기 위한 과정

1. Migration을 준비하는 과정
2. Migration을 적용하는 과정



---



## 테이블 생성하기 위한 과정

> pycharm 터미널에 명령어 입력

#### 1. DB Migration을 수행하는 앱을 `settingd.py` 파일 안의 `INSTALLED_APPS` 리스트에 등록

#### 2. `models.py`에 모델 클래스 작성

```
class 모델이름(models.Model):
	필드 이름1 = models.필드타입(필드옵션)
	필드 이름2 = models.필드타입(필드옵션)
```

#### 3. SQL을 수행하기 위한 파이썬 소스 생성

```
python manage.py makemigrations 앱이름
```

* 모델 소스를 읽고 생성될 DB 테이블의 SQL
* `migrations/0001_initial.py` 이 생성됨
* `models.py`가 수정되면 해당 명령어 다시 실행해야 반영됨

#### 3. 생성된 SQL을 실행시켜 SQLite에 테이블 생성

```
python manage.py migrate
```

 #### ... 이후 데이터베이스는 HeidSQL에서 확인 가능 (문서 참고)



---



## 테이블 조작하기

> Django는 데이터를 추가/갱신하고 읽어 들일 수 있는 다양한 데이터베이스 API 들을 자동으로 제공
>
> 이러한 기능은 Django가 ORM 서비스를 기본적으로 제공함에 따른 것으로 데이터베이스를 편리하게 핸들링할 수 있게 도와줌



#### INSERT

#### SELECT

#### UPDATE

#### DELETE



---



## INSERT

```python
모델클래스명(필드명1=필드값1, 필드명2=필드값2, ...).save()
```

* 모델 객체를 생성하고, 그 객체의 `save()` 메서드 호출
* 해당 메서드가 호출되면 SQL의 `INSERT`가 생성되고 실행되어 
* **테이블에 데이터가 추가됨**



---



## SELECT

```
모델클래스명.objects.메서드명()
```

* 데이터를 읽어오기 위해서는 Django 모델의 `Manager`, 즉 `모델클래스.objects` 사용해야 함!
  * Django는 디폴트로 모든 Django 모델 클래스에 대해 `objects` 라는 `Manager(django.db.models.Manager)` 객체를 자동으로 추가함
  * 이 `Manager`를 통해 특정 데이터 필터링, 정렬 등의 여러 기능들 사용 가능

#### 주요 메서드

> 아래의 쿼리 메서드들은 실제로 데이터 결과를 직접 리턴하는 것이 아니라,
>
> 쿼리 표현식(Django에서는 QuerySet이라고 함)을 리턴함
>
> 따라서 여러 메서드들을 체인처럼 연결하여 사용할 수 있음
>
> 여러 체인응로 연결되면 최종적으로 리턴된 쿼리가 해석되어 DB에는 하나의 최종 쿼리를 보내게 됨!

* `all()`
  * 테이블 데이터 전부 가져오기
  * `QuerySet` 객체가 리턴됨
* `get()`
  * 하나의 행(Row) 가져오기
  * 인자 : 행의 `pk값` 또는 `id값`
  * 예시 : `모델클래스명.objects.get(id=id값)`
* `filter()`
  * 특정 조건에 맞는 행(Row)들 가져오기
  * 예시 : `rows = 모델클래스명.objects.filter(name='김혜림')`
* `exclude()`
  * 특정 조건을 제외한 나머지 행(Row)들 가져오기
  * 예시: `rows = 모델클래스명.objects.exclude(name='김혜림')`
* `count()`
  * 데이터 갯수(Row 갯수)를 반환
* `order_by()`
  * 데이터를 키에 따라 정렬
  * 인자: 정렬 키
  * 내림차순 정렬 : 정렬 키 앞에 `-`를 붙이기
  * 예시 : `rows = 모델클래스명.objects.order_by('id', '-name')`
    * id를 기준으로 올림차순, name을 기준으로 내림차순 정렬

* `distinct()`
  * 중복된 값을 하나로만 표시
  * = SQL의 `SELECT DISTINCT`
  * 인자 : 필드명
* `first()`
  * 데이터들 중 처음에 있는 행(Row) 리턴
  * 예시 : `row = 모델클래스명.objects.order_by('name').first()`
* `last()`
  * 데이터들 중 마지막에 있는 행(Row) 리턴



---



## UPDATE

```
모델클래스명.필드명1 = 필드값1
모델클래스명.필드명2 = 필드값2
...
모델클래스명.save()
```



---



## 외래키 사용하기

#### Academy 모델 클래스

```python
from django.db import models

class Academy(models.Model) :
    name = models.CharField(max_length=45)
    address_full = models.CharField(max_length=80)
    address_city = models.CharField(max_length=45)
    address_town = models.CharField(max_length=45)
    fee1 = models.IntegerField(null=True)
    fee2 = models.IntegerField(null=True)
    bus = models.CharField(max_length=500, null=True)
    phone_number = models.CharField(max_length=45, null=True)
    url = models.CharField(max_length=500, null=True)
```

#### Academy_review 모델 클래스 (외래키 가짐)

```python
from django.db import models
from searchApp.models import Academy

class Academy_review(models.Model):
    title = models.CharField(max_length=45, default="제목없음")
    password = models.CharField(max_length=8)
    content = models.CharField(max_length=500)
    writedate = models.DateField(auto_now_add=True)
    academy_id = models.ForeignKey(Academy, on_delete=models.CASCADE)
```

* 예시

  * views.py

    ```python
    def review(request) :
        page = request.GET.get('page', 1)
    
        academyReview = Academy_review.objects.all()
        reviewPaginator = Paginator(academyReview, 5)
        reviewlistpage = reviewPaginator.get_page(page)
    
        context = {"academyReview": reviewlistpage}
        return render(request, 'review.html', context)
    ```

  * review.html

    ```html
     {% if academyReview %}
      <table class="table table-bordered">
        <thead>
    
        </thead>
        <tbody>
          {% for review in academyReview %}
          <tr>
            <td> {{ review.academy_id.name }} </td>
            <td> {{ review.academy_id.address_city }} </td>
            <td> {{ review.academy_id.address_town }} </td>
            <td> {{ review.title }} </td>
            <td> {{ review.writedate }} </td>
            <td><button onclick="confirmDelete('{{ review.pk }}')">삭제</button></td>
          </tr>
          {% endfor %}
        </tbody>
      </table>
      {% else %}
      <br>
      <h1>아직 내용이 없습니다</h1>
      {% endif %}
    ```

    

  ---

  

