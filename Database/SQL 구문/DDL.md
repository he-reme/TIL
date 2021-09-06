# DDL

>  Data Definition Language

* 데이터 정의어
* 데이터베이스 객체(table, view, index,...)의 구조를 정의
* 테이블 생성, 컬럼 추가, 타입변경, 제약조건 지정, 수정 등

<br>

---

<br>

## SQL문

#### create

* 데이터베이스 객체 생성

<br>

#### drop

* 데이터베이스 객체를 삭제

<br>

#### alter

* 기존에 존재하는 데이터베이스 객체를 수정

<br>

---

<br>

#### 데이터베이스 생성

```sql
create database 데이터에비스명;
```

```sql
create database 데이터베이스명
default character set 값
collate 값;
```

* Character set

  * 각 문자가 컴퓨터에 저장될 때 어떠한 '코드'로 저장될지에 대한 규칙의 집합을 의미

* Collation

  * 특정 문자 셋에 의해 데이터베이스에 저장된 값들을 비교 검색하거나 정렬 등의 작업을 위해 문자들을 서로 '비교'할 때 사용하는 규칙들의 집합을 의미

* 다국어 처리 (utf8mb3) : dbtest 생성

  ```sql
  create database dbtest
  default character set utf8mb3 collate utf8mb3_general_ci;
  ```

* 이모지 문자까지 처리

  ```sql
  create database dbtest
  default character set utf8mb4 collate utf8mb4_general_ci
  ```

<br>

---

<br>

#### 데이터베이스 변경

```sql
alter database 데이터베이스명
default character set 값 collate 값;
```

* dbtest의 character set, collate 변경

  ```sql
  alter database dbtest
  default character set utf8mb4 collate utf8mb4_general_ci
  ```

<br>

---

<br>

#### 데이터베이스 삭제

```sql
drop database 데이터베이스명;
```

<br>

---

<br>

#### 데이터베이스 사용

```sql
use 데이터베이스명;
```

<br>

---

<br>

#### 테이블 생성

```sql
create table table_name (
	column_name1 Type [optional attributes],
	column_name2 Type,
	.
	column_nameN Type,
);
```

* optional attributes

  * NOT NULL
    * 각 행은 해당 열의 값을 포함해야 하며 NULL값은 허용되지 않음
  * DEFAULT value
    * 값이 전달되지 않을 때 추가되는 기본값 설정
  * UNSIGNED
    * Type이 숫자인 경우만 해당되며 숫자가 0또는 양수로 제한됨
  * AUTO INCREMENT
    * 새 레코드가 추가 될 때마다 필드 값을 자동으로 1 증가시킴
  * PRIMARY KEY
    * 테이블에서 행을 고유하게 식별하기 위해 사용. PRIMARY KEY 설정이 있는 열은 일반적으로 AUTO INCREMENT와 같이 사용되는 경우가 많음

* 제약 조건

  * 컬럼에 저장될 데이터의 조건을 설정하는 것
  * 제약조건을 설정하면 조건에 위배되는 데이터는 저장 불가
  * 테이블 생성시 컬럼에 직접 지정하거나 constraint로 지정, 또는 alter를 이용해 설정 가능

  * 종류
    * NOT NULL
      * 컬럼에 NULL값을 저장할 수 없고, 반드시 쿼리문을 이용하여 값을 지정
    * UNIQUE
      * 컬럼에 중복된 값을 저장할 수 없음. NULL값은 허용
    * PRIMARY KEY
      * 기본키
      * 컬럼에 중복된 값을 저장할 수 없음
      * NULL값 허용 X
      * 주로 ROW를 구분하기 위한 유일한 값을 지정할 때 사용
    * FOREIGN KEY
      * 참조키, 외래키
      * 특정 테이블의 PK 컬럼에 저장되어 있는 값만 저장
      * NULL값 허용
      * references를 이용하여 어떤 컬럼에 어떤 데이터를 참조하는지 반드시 지정
    * DEFAULT
      * NULL값이 들어올 경우 기본 설정되는 값을 지정
    * CHECK
      * 값의 범위나 종류를 지정
      * MYSQL 8.0.16부터 사용 가능
        * 이전 버전의 경우 설정은 되나 적용이 안됨

<br>

---

<br>

#### ER Diagram (ERD)

* 개체 타입과 관계 타입을 기본 개념으로 현실 세계를 개념적으로 표현하는 방법