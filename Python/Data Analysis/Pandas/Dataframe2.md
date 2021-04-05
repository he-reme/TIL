# Dataframe 2

> 데이터프레임의 다양한 응용

 

---



## 함수 매핑

#### `apply` 함수

```
Series객체.apply(매핑함수)
df['열이름'].apply(매핑함수)
df.apply(매핑함수, axis=0) # 열 (기본값)
df.apply(매핑함수, axis=1) # 행
```

* Series, DataFrame에서 사용

* 각각의 행 또는 열단위로 함수 일괄 적용

* 매핑 함수로 `lamda` 함수 사용 가능

* 예시

  ```python
  def test_func(n):
  	return n+10
  	
  new_sr = sr.apply(test_func)
  new_sr = sr.apply(lamda x: x+10)
  ```

#### `map` 함수

```
sr.map(매핑함수)
```

* Series에서 사용
* 모든 요소에 함수 일괄 적용

#### `applymap` 함수

```python
df.applymap(매핑함수)
```

* DataFrame에서 사용
* 모든 요소에 함수 일괄 적용

#### `pipe` 함수

```python
df.pipe(매핑함수1).pipe(매핑함수2)
```

* DataFrame에서 사용
* 매핑함수가 반환하는 리턴값에 따라 pipe() 메소드가 반환하는 객체의 종류가 결정됨

---



## 열 재구성

#### 열 순서 변경

```python
df = df[재구성한 열 이름의 리스트]
```

* 열 이름을 알파벳 순으로 정렬하기

  ```python
  columns = list(df.columns.values)
  columns_sorted = sorted(columns)
  df = df[columns_sorted]
  ```

#### 열 분리

* 연, 월, 일 분리하기

```python
df['연월일'] = df['연월일'].astype('str')
dates = df['연월일'].str.split('-')
```

```python
df['연'] = dates.str.get(0)
df['월'] = dates.str.get(1)
df['일'] = dates.str.get(2)
```



---



## 필터링

#### 불린 인덱싱

```
df[불린 시리즈]
```

* 시리즈 객체에 어떤 조건식을 적용하면 각 원소에 대해 참/거짓을 판별하여 불린값으로 구성된 시리즈를 반환함

* 이때 참에 해당하는 데이터 값을 따로 선택할 수 있음

* 데이터프레임의 각 열은 시리즈 객체이므로, 조건식을 적용하면 각 원소가 조건을 만족하는지 여부를 참과 거짓 값으로 표시하여 불린 시리즈를 만들 수 있음

* 이 불린 시리즈를 데이터프레임에 대입하면 조건을 만족하는 행들만 선택할 수 있음

* `&` , `|` 

* 예시

  ```python
  import seaborn as sns
  
  titanic = sns.load_dataset('titanic')
  
  mask = (titanic.age >= 10) & (titanic.age < 20)
  
  df_teenage = titanic.loc[mask, :] # 모든 열
  df_teenage = titanic.loc[mask, ['열이름1', '열이름2']]
  ```

#### `isin` 메소드 활용

```python
df.isin(추출 값의 리스트)
```

* 데이터프레임의 열에 `isin()` 을 적용하면 특정 값을 가진 행들을 따로 추출할 수 있음

* 이때 `isin()` 에 데이터프레임의 열에서 추출하려는 값들로 만든 리스트를 전달한다.

* 예시

  ```python
  import seaborn as sns
  import pandas as pd
  
  titanic = sns.load_dataset('titanic')
  
  # 함께 탑승한 형제 또는 배우자의 수가 3, 4, 5인 승객만 추출
  isin_filter = titanic['sibsp'].isin([3, 4, 5])
  df_isin = titanic[isin_filter]
  ```

#### `filter` 메소드 활용

* 원하는 열만 추출

  ```
  df.filter(items=['열이름1', '열이름2'])
  ```

* 이름에 따른 추출

  ```python
  df.filter(regex='e$', axis=1) # e로 끝나는 열만 추출
  df.filter(regex='t$', axis=0) # t로 끝나는 인덱스만 추출
  df.filter(like='bbi', axis=0) # bbi가 포함된 인덱스만 추출
  df.filter(like='e', axis=1) # e가 포함된 열만 추출
  ```

#### `loc` 사용

* `열이름1>10` 혹은 `열이름2=='혜림'` 인 모든행 추출

  ```python
  df.loc[df.열이름1>10 | df.열이름2=='혜림', :]
  ```

* `열이름1>10` 그리고 `열이름2=='혜림'` 인 모든행 추출

  ```python
  df.loc[df.열이름1>10 & df.열이름2=='혜림', :]
  ```

  

---



## 데이터프레임 합치기

#### 데이터프레임 연결

 ```python
pd.concat(데이터프레임리스트)
 ```

* 서로 다른 데이터프레임들의 구성 형태와 속성이 균일하다면, 행 또는 열 중에 어느 한 방향으로 이어 붙여도 데이터의 일관성을 유지할 수 있음

* `axis`
  * `0` : 행(위아래로 연결), 기본값
  * `1` : 열(좌우로 연결)

* `join`

  * `outer` 옵션 : 열 이름에 대해서는 이 옵션이 기본 적용됨
    * 구성 형태와 속성이 균일하지 않은 경우 NaN 발생
  * `inner` 옵션 : 교집합으로 연결

* `ignore_index=True`

  * 기존 행 인덱스를 무시하고 새로운 행 인덱스를 설정

* 시리즈-시리즈, 데이터프레임-시리즈 연결

  * 열(좌우)로 연결

* 예시

  ```python
  pd.concat([df1, df2], axis=1, sort=True)
  ```

#### 데이터프레임 병합

```python
pd.merge(df_left, df_right, how='inner', on=None)
```

* SQL의 join명령과 비슷한 방식
* 키가 되는 열이나 인덱스가 반드시 양쪽 데이터프레임에 모두 존재해야 함
  * 키 : 기준이 되는 열이나 인덱스
* `on` 
  * 키
  * 두 데이터프레임 둘 다 가지고 있는 열이름
  * 이름이 다를 경우, 각각 지정 가능
    * `left_on`
    * `right_on`
* `how`
  * `inner` : 기본값
  * `outer`
  * `left`
  * `right`

```python
df.join()
```



---



## 그룹연산





---



## 멀티 인덱스



---



## 피벗

