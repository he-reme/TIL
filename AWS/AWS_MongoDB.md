# MongoDB

* **NoSQL**로 분류
  * Not Only SQL
  * MySQL처럼 전통적인 테이블-관계 기반의 RDBMS가 아니며,
  * SQL을 사용하지 않음
* 크로스 플랫폼 도큐먼트 지향 데이터베이스 시스템
* C++로 작성된 오픈소스 문서지향적 데이터베이스

#### MongoDB 사용

* 똑같은 조건으로 설계되었을 때 기존 RDBMS보다 속도가 굉장히 빠름
* MongoDB 사용하는 경우
  * 데이터 consistency가 거의 필요 없고, 조인 연산을 embed로 대체할 수 있는 경우
* MongoDB 사용하지 않는 경우
  * 저장되는 데이터가 은행 데이터같이 consistency가 매우 중요한 작업

#### 구조

* MYSQL의 테이블과 같이 스키마가 고정된 구조 대신, 
* **JSON 형태의 동적 스키마형 문서를 사용**
  * **BSON**이라 부름

#### Document

* MongoDB에서 가장 기본적인 데이터
* MySQL에서의 `row`에 해당
* 한 개 이상의 key-value 쌍으로 이뤄져 있음

#### Collection

* Document의 집합
* MySQL에서의 `table`에 해당

#### DB

* Collection의 집합



---



## SQL vs NoSQL

> 반대 개념 X, 경쟁 상대 X

* 많은 회사들이 두 타입 모두 동시에 사용함

* 데이터가 급격하게 늘어나는 형태라면, NoSQL이 도움됨

#### 스케일링에 좋은 NoSQL

* SQL

  * 시스템이 커져가면서, **Scale-Up** 형태로 DB 증설
  * 관계를 가지는 테이블들이 수평적으로 더 커진다는 의미
  * 기본에 사용하던 DB시스템보다 고성능의 DB시스템이 필요하게되고, 굉장히 덩치가 큰 DB 시스템이 된다는 의미
  * 비용 많이 증가, 관리 어려워짐

* NoSQL

  * 시스템이 커져가면서, **Scale-Out** 형태로 DB 증설
  * 고성능의 DB를 갖추는 것이 아닌
  * 여러 DB 시스템으로 추가할 수 있다는 의미

  * 숫자는 **무한대로 늘릴 수 있음**
    * SQL의 Scale-Up이 무제한적으로 늘려갈 수 없는 것과 비교해 **장점**이 됨



---



#### SQL - NoSQL

* 데이터베이스 - 데이터베이스
* 테이블 - 컬렉션
* 행 - 도큐먼트
* 열 - 필드
* 테이블 조인 - 임베디드 도큐먼트 & 링킹
* 인덱스 - 인덱스
* 주키 - 주키 (MongoDB에서는 _id 필드로 자동 설정됨)
* 집합(group by) -  집합 프레임워크



---



## NoSQL의 데이터 모델

* Document Store
  * 문서 저장소
  * 데이터 및 메타 데이터는 데이터베이스 내의 JSON 기반 문서에 계층적으로 저장
* Key-Value Store
  * 키 값 저장소
  * NoSQL 데이터베이스 중 가장 간단한 데이터는 키-값 쌍의 컬렉션으로 표시
* Wide-Column Store
  * Wide-Column 저장소
  * 관련 데이터는 단일 열에 중첩 키/값 쌍의 집합으로 저장
* Graph Store
  * 그래프 저장소
  * 데이터는 그래프 구조의 노드, 에지 및 데이터 속성으로 저장



---



## AWS에서 사용하기

#### MongoDB 실행

1. putty를 통해 AWS 서버 접속
2. `mongo` 명령어 입력

#### 원하는 데이터베이스 생성 및 사용하기

```
use 데이터베이스이름
```

 #### 현재 사용하고 있는 데이터베이스 확인하기

```
db
```

#### 데이터베이스 목록 확인하기

```
show dbs
```

* 막 신규 생성 돼서 데이터가 없는 데이터베이스는 안보임

#### 해당 컬렉션(테이블)에 데이터 삽입하기

```
db.컬렉션명.insert({"key1":value1, "key2":value2})
```

#### 해당 컬렉션(테이블) 모든 데이터 출력하기

```
db.컬렉션명.find()
db.컬렉션명.find().pretty() - 예쁘게 출력
```

#### 열 기준 정렬해 출력하기

```
db.컬렉션명.find().sort({"Key":1}) - 오름차순
db.컬렉션명.find().sort({"Key":-1}) - 내림차순
```

#### 조건 검색

```
db.컬렉션명.find({"key1":value1})
```



---



## Python에서 사용하기1

> \+ AWS의 MongoDB 접속

1. Putty를 통해 AWS 서버 접속
2. jupyter lab 실행 `AWS_test.md` 참고 

#### AWS의 MongoDB 접속

```python
from pymongo import MongoClient 
# 1
connection = MongoClient("mongodb://부여받은IP주소:27017/") 

# 2
mongo_server="부여받은IP주소"
connection = MongoClient(mongo_server, 27017)
```

```python
print(connection.list_database_names()) 
```

#### 접속 끊기

```python
connection.close()
```

#### 리눅스에 만들어놓은 데이터베이스의 book이라는 컬렉션의 도큐먼트들 추출

```python
my_doc = connection['데이터베이스이름']['book'].find()
for x in my_doc: 
   print(x)
```

#### 리눅스에 데이터베이스 생성 혹은 지정

```python
# 1
mydb = connection['데이터베이스명']
mycol = mydb['컬렉션명']
```

```python
 # 2
 mydb = connection.데이터베이스명
 mycol = mydb.컬렉션명
```

* 이미 있으면 지정, 없으면 생성됨

#### 데이터베이스의 컬렉션 리스트 출력하기

```python
collection_list = mydb.list_collection_names() 
print (collection_list)
```

#### 컬렉션의 도큐먼트(행) 출력

```python
# 한 개의 도큐먼트(행) 출력
x = mycol.find_one()
print(x)

# 여러 개의 도큐먼트(행) 출력
my_doc = mycol.find() 
for x in my_doc: 
   print(x)
```

#### 컬렉션에 도큐먼트(행) 추가

```python
# 하나만 추가
x = mycol.insert_one({"name":"gogildong", "address":"SSangmun-dong, Seoul"}) 
print(x.inserted_id)

# 여러개 추가
my_dict = [{"name":"ddochi", "address":"Seocho-dong, Seoul"}, 
           {"name":"dounar", "address":"Samsung-dong, Seoul"}, 
           {"name":"heedong", "address":"SSangmun-dong, Seoul"}] 
x = mycol.insert_many(my_dict) 
print(x.inserted_ids)
```

#### 특정 필드(열) 기준으로 정렬

```python
my_doc = mycol.find().sort("필드이름") 
for x in my_doc: 
   print(x)
```

* `sort("필드이름", -1) ` : 내림차순 정렬

#### 특정 도큐먼트(행) 추출

```python
my_query = {"address":"SSangmun-dong, Seoul"} 
my_doc = mycol.find(my_query) 
for x in my_doc: 
    print(x)
```

```python
# f 보다 뒤에 나오는 name들 추출
my_query = {"name":{"$gt":"f"}} 
my_doc = mycol.find(my_query) 
for x in my_doc: 
    print(x)
```

```python
# name 필드의 값이 d로 시작하는 것
my_query = {"name":{"$regex":"^d"}} 
my_doc = mycol.find(my_query) 
for x in my_doc: 
    print(x)
```

#### 특정 도큐먼트(행) value 바꾸기(update)

```python
mycol.update_one(
	{"찾을key":찾을value},
	{"$set" : {"바꿀value의 key": 바꿀value}}
)
```

```python
# id가 5인 데이터가 존재하면 {'id':'5','name':'kim'}로 update를 하고 존재하지 않으면 insert
test_collection.update_one({'id':'5'}, {'$set': {'id':'5','name':'kim2'}}, upsert=True) 
```

#### 특정 도큐먼트(행) 삭제

```python
# number이 6초과인 행만 찾아 삭제
test_collection.delete_many( {"number": { "$gt": 6 } } )
```



---



## 쿼리 옵션

* `$lt` : 미만
* `$lte` : 이하

* `$gt` : 초과
* `$gte` : 이상

* `$in` : 해당 리스트 중 하나라도 만족하는 거

  ```
  # occupation이 actor이거나 developer이면
  { 'occupation': {'$in': ["actor","developer"] } 
  ```

* `$nin` : `$in` 과 반대
* 등등 더 찾아보세요~