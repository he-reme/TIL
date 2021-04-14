# 함수

> SQL에서 사용할 수 있는 함수



---



## 집계 함수

> GROUP BY와 함께 사용

* SELECT, HAVING 절에서 사용

#### `SUM`

```mariadb
SELECT deptno, SUM(sal)
FROM emp
GROUP BY deptno;
```

#### `MAX`

```mariadb
SELECT deptno, MAX(sal)
FROM emp
GROUP BY deptno;
```

#### `COUNT`

```mariadb
SELECT job, COUNT(*)
FROM emp
WHERE deptno = 30
GROUP BY job;
```

* 해당하는 행 개수 셈



---



#### `date_format`

```mariadb
DATE_FORMAT(열이름, '%Y%m%d');
DATE_FORMAT(열이름, '%Y-%m-%d');
DATE_FORMAT(열이름, '%Y년 %m월 %d일');
DATE_FORMAT(열이름, '%Y');
DATE_FORMAT(열이름, '%m');
DATE_FORMAT(열이름, '%d');
DATE_FORMAT(열이름, '%H:%M');
DATE_FORMAT(열이름, '%H:%i:%S');
```

* SELECT, WHERE 절에서 사용 가능

* 사용 예시

  ```mariadb
  SELECT * 
  FROM emp 
  WHERE DATE_FORMAT(hiredate, '%Y') = '1982';
  ```



---



#### `concat`

```mariadb
concat(열이름, '문자열')
```

* 문자열 결합

* 해당 열의 값들에 해당 문자열을 붙여 출력함

* 사용 예시

  ```mariadb
  SELECT ename, concat(sal, '원') as sal
  FROM emp
  ORDER BY sal DESC;
  ```

  ```mariadb
  SELECT ename, concat(format(sal, 0), '원') 
  FROM edu18db.emp
  ORDER BY sal DESC;
  ```

  * `format`과 사용하면 1000단위로 콤마 찍어줌

  * `format(열이름, 소숫점아래자리수)`