# JOIN

* 둘 이상의 테이블에서 데이터가 필요한 경우 테이블 조인이 필요
* 일반적으로 조인 조건을 포함하는 WHERE절을 작성해야 함
* 조인 조건은 일반적으로 각 테이블의 PK및 FK로 구성됨

<br>

#### JOIN의 종류

* INNER JOIN
* OUTER JOIN
  * LEFT OUTER JOIN
  * RIGHT OUTER JOIN

<br>

#### JOIN 조건의 명시에 따른 구분

* NATURAL JOIN
* CROSS JOIN(FULL JOIN, CARTESIAN JOIN

<br>

#### JOIN시 주의

* 조인의 처리는 어느 테이블을 먼저 읽을 지를 결정하는 것이 중ㅇ
  * 처리할 작업량이 상당히 달라진다
* INNER JOIN
  * 어느 테이블을 먼저 읽어도 결과가 달라지지 않아 MySQL 옵티마이저가 조인의 순서를 조절해서 다양한 방법으로 최적화를 수행할 수 있음
* OUTER JOIN
  * 반드시 OUTER가 되는 테이블을 먼저 읽어야 하므로 옵티마이저가 조인 순서를 선택할 수 없음

<br>

---

<br>

## INNER JOIN

* 가장 일반적인 JOIN의 종류이며 교집합이다
* 동등 조인이라고도 함 (Equi-Join)
* **N개의 테이블 조인 시 N-1개의 조인 조건이 필요함**
  * 안그러면 카타시안 프로덕트결과가 나옴

<br>

#### 형식

```sql
SELECT COL1, COL2, ... , COLN
FROM table1 INNER JOIN table2
ON table1.column = table2.column;
```

* table에 alias 사용시

  ```sql
  SELECT alias1.COL1, alias1.COL2, ... , alias2.COLN
  FROM table1 AS alias1 INNER JOIN table2 AS alias2
  ON alias1.column = alias2.column;
  ```

* ON절 대신 USING 사용 가능

  ```sql
  SELECT COL1, COL2, ... , COLN
  FROM table1 INNER JOIN table2
  USING (공통 column);
  ```

  * table이름이나 alias를 명시하면 error

* 일반 조건절은 WHERE에, 
* JOIN 조건절은 ON/USING에

<br>

---

<br>

## NATURAL JOIN

* 알아서 INNER JOIN 해줌
* 단!!!! 두 테이블 간에 공통 COLUMN이 2개 이상인 경우 원하는 결과가 나오지 않을 수 있음!!!!
  * 모든 공통 COLUMN에 대해 JOIN 연산을 하기 때문에

<br>

#### 형식

```sql
SELECT COL1, COL2, ..., COLN
FROM table1 NATURAL JOIN table2;
```

<br>

---

<br>

## OUTER JOIN

* 구분
  * LEFT OUTER JOIN
  * RIGHT OUTER JOIN
  * FULL OUTER JOIN : MySql은 지원 안함
* 어느 한쪽 테이블에는 해당 데이터가 존재하는데 다른 쪽 테이블에는 데이터가 존재하지 않을 경우 그 데이터가 검색되지 않는 문제점을 해결하기 위해 사용
* 사용할 때 그냥 `JOIN` 키워드만 써도 됨

<br>



