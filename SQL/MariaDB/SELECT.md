# SELECT

* 환경
  * HeidSQL
  * MariaDB



---



## 기본 구조

```mariadb
SELECT 
FROM
WHERE
GROUP BY
HAVING
ORDER BY
```

#### 실행 순서

`FROM` > `WHERE` > `GROUP BY` > `HAVING` > `SELECT` > `ORDER BY`

#### 예시

```
SELECT job, COUNT(*)
FROM emp
WHERE deptno = 30
GROUP BY job
HAVING COUNT(*) > 2;
```

* emp 테이블에서
* depno가 30인 행만 추출하고
* job으로 그룹을 묶고,
* 해당 그룹마다 행 갯수가 2개보다 큰 그룹만 추출하여
* job그룹과 해당 그룹의 행 갯수 출력



---



## SELECT

> 열 선택

```mariadb
SELECT *
SELECT 열이름
```

* `*` 은 모든 열 선택

#### 별칭

```mariadb
SELECT 열이름 as 별칭
SELECT 열이름 별칭
SELECT 열이름 "별 칭"
```

* 이름에 공백 있는 경우에는 `""` 를 사용

#### 중복 처리

```mariadb
SELECT distinct 열이름
```

* 중복되는 값 한 번씩만 출력되도록 처리 

---



## FROM

> 테이블 선택

```mariadb
FROM 테이블명
FROM 데이터베이스명.테이블명
```



---



## WEHRE

> 조건

```mariadb
WHERE 열이름 > 30
WHERE 열이름 = '혜림'
```

#### 패턴 문자

```mariadb
WHERE ename = 'King' OR ename='Kang' OR ename='Kong'
WHERE ename IN ('King', 'Kang', 'Kong')
WHERE ename LIKE 'K%'
```

* `%` : 0개 이상의 임의의 문자
* `_` : 임의의 한 문자

#### 조건식 작성

* `AND`

* `OR`

* `IN`

  ```mariadb
  WHERE deptno IN (10, 20)
  ```

  * 부서번호가 10이나 20 이면

* `BETWEEN`

  ```mariadb
  WHERE sal BETWEEN 2000 AND 3000
  ```

  * 월급이 2000 ~ 3000 이면



---



## GROUP BY

> 그룹

```mariadb
GROUP BY 열이름
GROUP BY 열이름1, 열이름2, ...
```

* 집계 함수를 같이 사용함

  * `SUM`

  

#### 사용 예시

```mariadb
SELECT deptno, SUM(sal)
FROM emp
GROUP BY deptno;
```

* SELECT 할 때

  * **그룹으로 묶은 열 이름을 먼저 놓는게 좋음!**

  * 그룹 단위가 아닌, 행 단위로 나오는 열은 SELECT 하면 안됨!

    ```mariadb
    -- 잘못된 예시
    SELECT deptno, SUM(sal), ename
    FROM emp
    GROUP BY deptno;
    ```



---



## HAVING

> 그룹에 대한 조건절

```
HAVING 집계함수를 이용한 조건절
```

#### 사용 예시

```
SELECT deptno, SUM(sal)
FROM emp
GROUP BY deptno
HAVING SUM(sal) > 10000;
```

* HAVING 절의 조건에 맞는 그룹만 추출



---



## ORDER BY

> 정렬

```mariadb
ORDER BY 열이름 ASC
ORDER BY 열이름 DESC
```

* `ASC`는 생략 가능



---



## 집합 연산

```
SELECT절(1)
집합연산
SELECT절(2)
```

#### UNION all

* 합집합

* SELECT절(1) 결과값과 SELECT절(2) 결과값의 합집합을 출력

#### UNION

* 합집합

* SELECT절(1) 결과값과 SELECT절(2) 결과값을 합집합을 출력

* 단, 중복 처리하면서 붙임

#### INTERSECT

* 교집합
* SELECT절(1) 결과값과 SELECT절(2) 결과값의 교집합을 출력

#### EXCEPT

* 차집합
* SELECT절(1) 결과값과 SELECT절(2) 결과값의 차집합을 출력



---



## 출력

#### `LIMIT`

```mariadb
LIMIT 출력 갯수
```

* 출력 갯수 조절

#### `OFFSET`

```mariadb
LIMIT 출력 갯수 OFFSET 출력을 시작할 행번호
```

* 생략 시 처음부터 출력 : `0`

#### 사용 예시

```mariadb
SELECT *
FROM emp
ORDER BY sal DESC
LIMIT 3 OFFSET 3;
```

* 4번행부터 3개 출력