# MariaDB

> MySQL과 유사



---



## 기본 DB 구조

#### CRUD

* C

  ```mariadb
  insert into 테이블명 [(컬럼명리스트, ...)] values (데이터값리스트, ...)
  ```

* R

  ```mariadb
  select 컬럼명, ...
  [from 테이블명
  where 조건식
  group by 그룹핑기준컬럼, ...
  having 그룹조건
  order by 정렬기준컬럼 [desc]	, ...]
  ```

* U

  ```mariadb
  update 테이블명 set 컬럼명=컬럼값, ... [where 조건식]
  ```

* D

  ```mariadb
  delete [from] 테이블명 [where 조건식]
  ```
