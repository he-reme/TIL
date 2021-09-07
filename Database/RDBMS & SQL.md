# RDBMS & SQL

#### RDBMS

* 관계형 데이터베이스 시스템
* 테이블기반의 DBM
  * 데이터를 테이블 단위로 관리
    * 하나의 테이블은 여러 개의 컬럼으로 구성
  * 중복 데이터를 최소화 시킴
    * 같은 데이터가 여러 컬럼 또는 테이블에 존재 했을 경우, 데이터를 수정 시 문제가 발생할 가능성이 높아짐 - 정규화
  * 여러 테이블에 분산되어 있는 데이터를 검색 시 테이블 간의 관계를 이용하여 필요한 데이터를 검색

<br>

#### SQL

* Structured Query Language
* 데이터베이스에 있는 정보를 사용할 수 있도록 지원하는 언어
* 모든 DBMS에서 사용 가능
* **대소문자는 구별하지 않음**
  * 단, 데이터의 대소분자는 구분

* SQL 구문
  * DCL, DDL, DML

<br>

#### DESC

* 테이블 구조 확인

<br>

---

<br>

## SQL 구문

#### DML

* Data Manipulation Language
* 개별적으로 Database 테이블에서 새로운 행을 입력하고, 기존의 행을 변경하고 제거, 데이터 검색

* 문장
  * INSERT, UPDATE, DELETE, SELECT

<br>

#### DDL

* Data Definition Language
* 테이블로부터 데이터 구조를 생성, 변경, 제거
* 문장
  * CREATE, ALTER, DROP, RENAME

<br>

#### DML

* 문장
  * COMMIT, ROLLBACK

<br>

#### DCL

* Data Control Language
* 데이터베이스와 그 구조에 대한 접근권한을 제공하거나 제거
* 문장
  * GRANT, REVOKE

<br>

---

<br>

## DCL

> Data Control Language

* 데이터 제어어
* DB, Table의 접근권한이나 CRUD 권한을 정의
* 특정 사용자에게 테이블의 검색권한 부여/금지 등

<br>

#### SQL문

* grant
  * 데이터베이스 객체에 권한을 부여
* revoke
  * 데이터베이스 객체 권한 취소

<br>

---

<br>

## TCL

> Transaction Control Language

* 트랜잭션 제어어
* transaction
  * 데이터베이스의 논리적 연산 단위

<br>

#### SQL문

* commit
  * 실행한 Query를 최종적으로 적용
* rollback
  * 실행한 Query를 마지막 commit 전으로 취소시켜 데이터를 복구

<BR>

<br>

---

<br>

## Data Type

#### 문자형 데이터 타입

* `CHAR[(M)]`
  * 고정 길이를 갖는 문자열을 저장
* `VARCHAR[(M)]`
  * 가변 길이를 갖는 문자열을 저장
  * CHAR보다 더 긴 길이의 문자열 저장 가능
* `TEXT[(M)]`

* `INT((M))`

* `DOUBLE[(M,D)]`
  * M : 자릿수
  * D : 소수점의 자릿수
* `DATE`
  * YYYY-MM-DD
* `TIME`
  * HH:MM:SS
* `DATETIME`
  * YYYY-MM-DD HH:MM:SS
* `TIMESTAMP[(M)]`
  * local 시간
  * 일반적으로 `DATETIME`보다 더 많이 사용함

* BLOB[(M)]
  * 사진이나 영화 저장