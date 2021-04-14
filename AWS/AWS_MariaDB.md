## MariaDB 사용

> AWS



---



## MariaDB 연동

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



---



## Cursor 객체 생성

* 연결한 DB와 상호작용하기 위해 `cursor` 객체 생성해줘야 함

#### Cursor 종류

* 일반 Cursor
  * 결과를 **튜플** 형태로 반환
* DictCursor
  * 결과를 **딕셔너리** 형태로 반환
  * 주로 데이터 분석가는 데이터프레임 형태로 결과를 쉽게 변환할 수 있도록 이 커서를 사용함

