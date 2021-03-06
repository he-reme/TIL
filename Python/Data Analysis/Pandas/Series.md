# 시리즈

> 1차원 배열

#### 시리즈 만들기

```python
sr = pandas.Series(딕셔너리/리스트/튜플)
```

* 딕셔너리를 시리즈로 변환하는 방법을 많이 사용
  * 딕셔너리와 시리즈의 구조가 비슷하기 떄문
* **딕셔너리**로 시리즈를 만들면
  * 딕셔너리의 키 → 인덱스
  * 딕셔너리의 값 → 데이터의 값
* **리스트/튜플**로 시리즈를 만들면
  * 인덱스가 별도로 정의하지 않으면
    * 디폴트로 `0`부터 자동 지정됨
  * 인덱스를 별도로 정의
    * `sr = pd.Series(list, index=['이름', '생년월일', '성별'])`

#### 인덱스 종류 (2가지)

* **정수형 위치 인덱스** (0부터 시작)
  * 접근
    * `[]` 
  * 범위로 줬을 때 
    * `[start:end]` 
    * end 값은 포함 X
  * 예시
    * `[1, 3] `, `[1:3]`
  * `[-1]` : 마지막 인덱스
  
* **인덱스 이름 / 인덱스 라벨**
  * 접근
    * `['라벨']` / `["라벨"]`
  * 범위로 줬을 때
    * `[start:end]`
    * end 값도 포함 O
  * 예시
    * `['a', 'b']` / `['a':'d']`

#### 속성

* `sr.index`
  * 시리즈의 인덱스 배열 확인
* `sr.values`
  * 시리즈의 데이터 값의 배열 확인



---



## 연산

> 연산자 : `+` `-` `*` `/`

#### 시리즈 vs 숫자

`sr + 연산자 + 숫자`

#### 시리즈 vs 시리즈

`sr1 + 연산자 + sr2`

* 같은 인덱스를 가진 원소끼리 계산
* 해당 인덱스에 연산 결과를 매칭하여 새 시리즈를 반환

* 두 시리즈의 원소 개수가 다르거나, 시리즈의 크기가 같더라도 인덱스 값이 다른 경우
  * `NaN`으로 처리
* 같은 인덱스가 양쪽에 모두 존재하여 서로 대응되어도, 어느 한 쪽의 데이터 값이 `NaN`인 경우
  * `NaN`으로 처리

#### 연산 메소드 활용

* 객체 사이에 공통 인덱스가 없는 경우 `NaN`으로 반환하는 상황을 피하기 위해 사용
* 연산 메소드에 `fill_value` 옵션 설정
  * `fill_value = NaN일 경우 채울 값`

* 연산 메소드
  * `sr1.add(sr2, fill_value=0)`
  * `sr1.sub(sr2, fill_value=0)`
  * `sr1.mul(sr2, fill_value=0)`
  * `sr1.div(sr2, fill_value=0)`