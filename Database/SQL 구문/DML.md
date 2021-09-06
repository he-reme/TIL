# DML

> Data Manipulation Language

* 데이터 조작어
* Data 조작 기증
* 테이블의 레코드를 CRUD
  * Create, Retrieve, Update, Delete

<br>

---

<br>

#### SQL문

#### insert (C)

* 데이터베이스 객체에 데이터를 입력

<br>

#### select (R)

* 데이터베이스 객체에서 데이터를 조회

<br>

#### update (U)

* 데이터베이스 객체에 데이터를 수정

<br>

#### delete (D)

* 데이터베이스 객체에 데이터를 삭제

<br>

---

<br>

#### INSERT

* 방법 1

  ```sql
  INSERT INTO table name
  VALUES (col_val1, col_val2, col_val3, ..., col_valN);
  ```

  * 컬럼 갯수만큼 값을 줘야 함

* 방법 2

  ```sql
  INSERT INTO table_name (col_name1, col_name2, col_name3, ... , col_nameN)
  VALUES (col_val1, col_val2, col_val3, ..., col_valN);
  ```

* 방법 3

  ```sql
  INSERT INTO table_name (col_name1, col_name2, col_name3, ... , col_nameN)
  VALUES (col_val1, col_val2, col_val3, ..., col_valN),
         (col_val1, col_val2, col_val3, ..., col_valN);
  ```

* 생략이 가능한 field
  * NULL이 허용된 컬럼
  * DEFAULT가 설정된 컬럼
  * AUTO INCREMENT가 설정된 컬럼

<br>

---

<br>

#### UPDATE

```sql
UPDATE table_name
SET col_name1 = col_val1, [col_name2 = col_val2, ... , col_nameN = col_val[N]]
WHERE conditions;
```

* WHERE절의 conditions(조건)에 만족하는 레코드의 값을 변경
* 주의 : **WHERE절을 생략하면 모든 데이터가 바뀜**

<br>

---

<br>

#### DELETE

```sql
DELETE from table_name
WHERE conditions;
```

* WHERE절의 conditions(조건)에 만족하는 레코드의 값을 삭제
* 주의 : **WHERE절을 생략하면 모든 데이터가 삭제됨**

<br>

---

<br>

## SELECT

```sql
SELECT * |{[ALL|DISTINCT] column_name | expression [alias], ...}
FROM table_name;
WHERE conditions;
ORDER BY col_name [ASC|DESC] [,col_name2, ...];
```

* SELECT 절과 FROM 절은 필수
* 실행 순서
  * FROM > WHERE > SELECT > ORDER BY

<br>

#### SELECT 절

* `*`
  
  * FROM 절에 나열된 테이블에서 모든 열을 선택
  
* ALL
  * 선택된 모든 행을 반환. 
  * ALL이 default (생략 가능)
  
* **DISTINCT**
  * 선택된 모든 행 중에서 **중복 행 제거**
  
* column
  * FROM 절에 나열된 테이블에서 지정된 열을 지정
  
* expression
  * 표현식은 값으로 인식되는 하나 이상의 값, 연산자 및 SQL 함수의 조합을 뜻함
  
* alias
  * 별칭
  * 가능하면 이렇게 사용하자..
    * data는 `' '`
    * 별칭은 `" "`
  
* 사용

  * alias
  * 사칙연산(+, -, *, /)
  * NULL Value

  * if문

    ```
    CASE exp1 WHEN exp2 THEN exp3
    		  [WHEN exp4 Then exp5
    		  ...
    		  ELSE exp6]
    END
    ```

<br>

#### WHERE 절

* 조건에 만족하는 행을 검색

* `AND`, `OR`, `NOT`

* * NULL 연산 주의
* `IN`
  * `WHERE 컬럼명 IN (50, 60, 70)`

* `BETWEEN`
  * `WHERE 컬럼명 BETWEEN 6000 AND 10000`

* NULL 비교
  * `IS NULL`, `IS NOT NULL`

* `LIKE (wild card : % , _)`
  * `%`
    * 갯수 제한 X
    * `WHERE 컬럼명 LIKE '%hello%'`
  * `_`
    * 갯수 제한
    * `WHERE 컬럼명 LIKE 'x__'`
      * xin, xoo, ...
      * xdkfjkjasdf (X)

<br>

#### ORDER BY 절

* 정렬
* 기본값 : ASC

<br>

#### GROUP BY 절

* SELECT문에 사용 가능한 컬럼
  * GROUP BY에 사용된 컬럼
  * 집계함수를 사용한 컬럼

<br>

#### Having 절

* 

<br>

#### limit

* 상위 N 까지 뽑기
  * `limit N`
* 상위 N부터 M개 뽑기
  * `limit N-1, M`

