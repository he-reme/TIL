## MariaDB 사용

> AWS

#### 순서

1. MariaDB 연동
2. Cursor 객체 생성
3. SQL 실행
4. SQL 실행 결과 출력



---



## 1. MariaDB 연동

> pymysql 이용
>
> `connect()` 함수 이용하면 MySQL host 내 DB와 직접 연결할 수 있음

```python
import pymysql
conn = pymysql.connect(host='DB가 존재하는 host',port=3306,user='유저이름',passwd='패스워드', db='db이름')
print(conn)
```

* `host`
  * DB가 존재하는 host
* `user` 
  * 유저 이름
* `passwd`
  * 설정한 패스워드
* `db`
  * 연결할 데이터베이스 이름
* `charset`
  * 인코딩 설정

#### DictCursor 지정

```python
import pymysql
conn = pymysql.connect(host='DB가 존재하는 host',port=3306,user='유저이름',passwd='패스워드', db='db이름', cursorclass = cursorclass=pymysql.cursors.DictCursor)
print(conn)
```



---



## 2. Cursor 객체 생성

>  연결한 DB와 상호작용하기 위해 `cursor` 객체 생성해줘야 함

```python
cur = conn.cursor()
```

#### Cursor 종류

* 일반 Cursor

  * 결과를 **튜플** 형태로 반환
  * `connect` 할 때, 따로 지정 없으면 자동 지정됨

* **DictCursor**

  * 결과를 **딕셔너리** 형태로 반환
  * 주로 데이터 분석가는 **데이터프레임 형태로 결과를 쉽게 변환할 수** 있도록 이 커서를 사용함

  * `connect` 할 때, `cursorclass = cursorclass=pymysql.cursors.DictCursor`  추가해주면 지정됨

  

---



## 3. SQL 실행

> SQL문을 변수에 넣어주고 `corsor.execute()` 을 사용해 실행

```python
sql = 'SELECT * FROM emp'
cur.execute(sql)
```



---



## 4. SQL 실행 결과 받아오기

> `fetchall()`, `fetchone()` 등으로 받아옴

```python
result = cur.fetchall()
result = cur.fetchone()
result = cur.fetchmany(n)
```

* `fetchall()` : 모든 데이터를 한 번에 가져올 때 사용
* `fetchone()` : 한 번 호출에 하나의 행만 가져올 때 사용
* `fetchmany(n)` :   n개 만큼의 데이터를 가져올 때 사용



---



## 연결 끊기

```python
conn.close()
```



---



## 사용 예시

```python
import pymysql
conn = pymysql.connect(host='DB가 존재하는 host',port=3306,user='유저이름',passwd='패스워드', db='db이름')

cur = conn.cursor()

sql = 'SELECT * FROM emp'
cur.execute(sql)

result = cur.fetchall()

conn.close()
```

