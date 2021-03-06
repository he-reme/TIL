# Database

> 특정 조직 내에서 다수의 사용자들이 공유해 사용할 수 있도록 통합하고 저장한 **운영 데이터의 집합체**

* Django의 데이터베이스는 Django>Model에 설명



---



## 데이터의 분류

#### 정형 데이터

* 구조화된 데이터
* 미리 정해준 구조에 따라 저장된 데이터
* 예
  * 엑셀의 스프레드 시트
  * 관계 데이터베이스 테이블
  * CSV

#### 반정형 데이터

* 구조에 따라 저장된 데이터이지만 데이터 내용 안에 구조에 대한 설명이 함께 존재
* 구조를 파악하는 파싱 과정 필요
* 예
  * HTML
  * XML
  * JSON
  * 웹 로그
  * 센서 데이터

#### 비정형 데이터

* 정해진 구조가 없이 저장된 데이터

* 예

  * 멀티미디어 데이터!
  * 소셜 데이터의 텍스트
  * 영상, 이미지
  * 워드, PDF 문서

  

---



## DBMS

> 데이터베이스 관리 시스템

* 데이터베이스를 생성하여 안정적이고 효율적으로 운영하는 데 필요한 기능들을 제공하는 소프트웨어

#### 종류

* **액세스** : 윈도우즈 플랫폼으로 중소 규모 데이터베이스를 위한 데스크톱용 DBMS
* **SQL 서버** : 저렴한 제품 가격으로 Windows NT 플랫폼에서 최적의 성능을 발휘
* 인포믹스 : 성능이 뛰어나며 병렬 처리를 위한 멀티스레드 지원
* **DB2** : 다수 사용자가 다수 관계형 데이터베이스를 동시에 접근할 수 있는 대형 데이터베이스를 위한 시스템
* **Oracle** : PC급에서 메인 프레임급까지 모두 설치할 수 있으며 분산 처리 지원 기능이 우수
* **MySQL** : 다양한 플랫폼과 API를 지원하는 비상업용 DBMS
  * **Maria DB** 와 유사 ㅎㅅㅎ



---



## 데이터베이스 사용자

* 일반 사용자
* 응용 프로그래머
* 데이터베이스 관리자



---



## 데이터베이스 특징

#### 데이터의 중복성을 최소화 할 수 있다

업무의 흐름에 따라 데이터를 통합 및 분리하여 관리할 수 있게 되므로 중복성을 줄임

#### 데이터의 일관성을 유지할 수 있다

데이터의 불일치성을 미리 방지하여 데이터를 정확하게 만들고 사용자에게 신뢰할 만한 정보를 제공

#### 데이터의 무결성을 유지할 수 있다

제약조건에 맞지 않는 데이터는 아예 입력되지 않도록 방지하는 기능을 제공해 데이터베이스의 무결성을 유지

* 무결성
  * 데이터베이스에 정확한 데이터가 유지되고 있음을 보장하는 것
  * 데이터베이스에서 가장 중요한 개념

#### 데이터의 독립성을 유지할 수 있다

테이터를 테이블 구조로 관리하기 때문에 독립성을 더욱 강화할 수 있음

* 독립성
  * 데이터의 표현 방법이나 저장 위치가 변하더라도 응용 프로그램에는 아무런 영향을 미치지 않는 것

#### 데이터의 공유성을 최대화할 수 있다

데이터베이스는 공동작업에 맞게 구조적으로 설계되며 통합된 체계에 의해 저장된 값들이 유지, 관리 되어야 하며, 조직의 구성원들은 응용 프로그램을 통해 데이터베이스에 저장된 공유 데이터들로부터 각자의 업무에 필요한 정보를 생성

#### 데이터의 보안성을 최대화 할 수 있다

데이터베이스 시스템의 성능을 평가하는 중요한 요소로, 최근 대부분의 데이터베이스 시스템은 이러한 보안 기능을 제공

#### 데이터를 표준화하여 관리할 수 있다

데이터를 사용 목적 등의 유형별로 분류해 데이터의 형식이나 길이, 이름 등을 설정



---



## 데이터 모델

#### 개념적 데이터 모델

* 개체 관계 모델

#### 논리적 데이터 모델

* 관계 데이터 모델
* 계층 데이터 모델
* 네트워크 데이터 모델



---



## E-R 모델링

관계 데이터 모델을 ERD 표기법 중 정보 공학 표기법으로 나타낸 것

* [ERD 작성 무료 웹](https://aquerytool.com/)



---



## 관계형 데이터 베이스

> 관계형 데이터 모델 사용
>
> 현재까지 가장 안정적이고 효율적인 데이터베이스

* 개체를 데테이블로 사용하고 개체들 간의 공통 속성을 이용해 서로 연결
* 자료의 구조가 단순한 업무에 적합

### 구성 요소

* 테이블

  * 릴레이션 혹은 엔티티
  * 열과 행으로 구성됨

* 필드

  * 속성 혹은 컬럼
  * 열에 해당
  * 데이터 값을 기억하는 기억 단위

* 레코드

  * 카디널리티
  * 투플, 행에 해당

* 후보키

  * 한 테이블 내에서 데이터 레코드를 고유하게 식별할 수 있는 필드

* 기본키

  * 후보 키 중에서 대표로 선정된 키
  * primary key

* 참조키(외래키)

  * 관계가 설정된 다른 테이블의 기본 키를 참조하는 키

    

---



## 데이터 제약 조건

> 무결성

#### 개체 무결성

* 기본키로 제약조건을 지정한 속성은 공백(NULL) 값이나 중복된 값을 가질 수 없음

#### 참조 무결성

* 외래 키를 통해 릴레이션이 참조할 수 없는 외래 키 값을 가질 수 없도록 함으로써 두 테이블 간의 데이터 무결성을 유지하는 것
* 외래키 값은 NULL이거나 참조 릴레이션의 기본키 값과 동일해야 함



---



## 정규화

> 불필요한 데이터의 중복을 피하고
>
> 이상현상을 방지하기 위해 테이블을 분해하는 과정

#### 데이터 중복의 문제점

* 데이터를 중복 저장하는 경우에는 데이터 변경에 의해 원하지 않던 결과가 발생할 수 있음
* 이를 **이상현상**이라고 함

#### 이상 현상

1.  삽입 이상

2. 삭제 이상

3. 수정 이상



---



## 관계 유형

> 표현 방법

* 일대일 (1:1)
* 일대다 (1:N)
* 다대다 (N:M)