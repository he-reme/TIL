# 데이터 전처리

#### 목차

* 누락 데이터 처리
* 중복 데이터 처리
* 데이터 표준화
* 범주형(카테고리) 데이터 처리
* 정규화
* 시계열 데이터



---



## 누락 데이터 처리

> 결측치 처리
>
> 대부분 새로운 dataframe을 반환

```python
import seaborn as sns
df = sns.load_dataset('titanic')
```

#### 1. 누락 데이터 확인

* 방법1

  ```python
  display(df.head())
  ```

* 방법2

  ```python
  print(df.info())
  ```

* 방법3

  ```python
  nan_deck = df['deck'].value_counts(dropna=False)
  print(nan_deck)
  ```

  * deck라는 열의 NaN 갯수 확인

* 방법4

  ```python
  df.isnull() # 누락 데이터면 True, 존재하면 False
  df.notnull() # 누락 데이터면 False, 존재하면 True
  ```

  ```python
  df.isnull().sum(axis=0) # sum()은 True인 갯수 반환
  ```

  * 누락 데이터의 갯수 반환

#### 2. 누락 데이터 처리

* **누락 데이터 제거**

  * 누락 데이터가 들어있는 행 제거

    ```python
    df = df.dropna(axis=0)
    ```

    * 특정 열로 한정하기

      ```python
      df = df.dropna(subset=['열이름'], axis=0)
      ```

  * 누락 데이터가 들어있는 열 제거

    ```python
    df = df.dropna(axis=1)
    ```

  * `thresh=갯수` 옵션

    * NaN가 갯수가 이상 있는 행, 열만 삭제함

  * `how='명령'` 옵션
    * `'all'` : 모두 NaN이면 삭제
    * `'any'` : 하나라도 NaN이면 삭제

* **누락 데이터 치환**

  ```python
  df['열이름'].fillna(대체값, inplace=True)
  ```

  * `method='명령'` 옵션

    * `'ffill'`
      * NaN이 있는 행의 직전 행에 있는 값으로 치환
    * `'bfill'`
      * NaN이 있는 행의 바로 다음 행에 있는 값으로 치환

  * 예시1 (평균값으로 치환하기)

    ```python
    mean_age = df['age'].mean(axis=0)
    df['age'].fillna(mean_age, inplace=True)
    ```

  * 예시2 (최빈값으로 치환하기)

    ```python
    most_freq = df['age'].value_counts(dropna=True).idxmax()
    df['age'].fillna(most_freq, inplace=True)
    ```

    

---



## 중복 데이터 처리

#### 1. 중복 데이터 확인

```python
df_dup = df.duplicated()
```

* 전에 나온 행들과 비교하여 중복되는 행이면 `True` 반환, 아니면 False 반환

* 특정 열만 확인하기

  ```python
  df_dup = df['열이름'].duplicated()
  ```

#### 2. 중복 데이터 제거

```python
df = df.drop_duplicates()
```

* `subset=['열이름1', '열이름2', ...]` 옵션
  * 특정 열만 중복 판별하고 삭제하기



---



## 데이터 변환

#### 단위 환산

* 같은 데이터셋 안에서 서로 다른 측정 단위를 사용한다면, 전체 데이터의 일관성 측면에서 문제가 발생함
* 같은 단위로 변환하자!

#### 자료형 변환

* 데이터의 자료형을 확인하고 적절한 자료형으로 변환하자!



---



## 범주형(카테고리) 데이터 처리

#### 구간 분할

* 데이터 분석 알고리즘에 따라서 연속 데이터를 그대로 사용하기 보다는 일정한 구간으로 나눠서 분석하는 것이 효율적인 경우가 있음
* 구간 분할 : 연속 변수를 일정한 구간으로 나누고, 각 구간을 범주형 이산 변수로 변환하는 과정

```python
bin_drivers = np.histogram(df['열이름'], bins=3)
bin_names = ['범주1', '범주2', '범주3'] # 원하는 이름으로 지정
```

```python
df['새로추가열'] = pd.cut(x=df['열이름'], # 데이터 배열
				   bins=bin_drivers, # 경계값 리스트
				   labels=bin_names, # bin 이름
				   include_lowest=True) # 첫 경계값 포함
```



#### 더미 변수

* 카테고리를 나타내는 범주형 데이터를 회귀분석 등 머신러닝 알고리즘에 바로 사용할 수 없는 경우가 있음
* 그래서 컴퓨터가 인식 가능한 입력값으로 변환해야 함
* 이럴 때 숫자 `0` 또는 `1`로 표현되는 `더미 변수`를 사용함.
  * `0`과 `1`은 어떤 특성이 있는지 없는지 여부만을 표시함
* `get_dummies()` 함수 사용
  * 범주형 변수의 모든 고유값을 각각 새로운 더미 변수로 변환함
  * 각 더미 변수가 본래 속해 있던 행에는 `1`, 속하지 않았던 다른 행에는 `0`이 입력됨

```python
bin_drivers = np.histogram(df['열이름'], bins=3)
bin_names = ['범주1', '범주2', '범주3'] # 원하는 이름으로 지정
```

```python
df['새로추가열'] = pd.cut(x=df['열이름'], # 데이터 배열
				   bins=bin_drivers, # 경계값 리스트
				   labels=bin_names, # bin 이름
				   include_lowest=True) # 첫 경계값 포함
```

```python
dummis = pd.gt_dummies(df['새로추가열'])
```



---



## 정규화

* 각 변수에 들어있는 숫자 데이터의 상대적 크기 차이 때문에 머신러닝 분석 결과가 달라질 수 있음
* 따라서 숫자 데이터의 상대적인 크기 차이를 제거할 필요가 있음
* 정규화 : 각 열에 속하는 데이터값을 동일한 크기 기준으로 나눈 비율로 나타내는 것
  * 정규화 과정을 거친 데이터의 범위
    * `0` ~ `1`  또는 `-1 ` ~ `1`

#### Min-Max scailling

* 각 열의 데이터 중에서 최대값과 최소값을 뺀 값으로 나누는 방법



---



## 시계열 데이터

> 날짜와 시간

* `Timestamp` : 특정한 시점을 기록하는 객체
* `Period` : 두 시점 사이의 일정한 기간을 나타내는 객체

#### 다른 자료형을 시계열 객체로 변환

* 판다스는 다른 자료형으로 저장된 시간 데이터를 판다스 시계열 객체인 `Timestamp`로 변환하는 함수를 제공

* **문자열(object)을 Timestamp로 변환**

  ```python
  df['새로운열이름'] = pd.to_datetime(df['변환하고싶은열이름'])
  ```

  * 판다스 Timestamp를 나타내는 `datetime64` 자료형으로 변환됨

  * `format` 옵션

    ```python
    pd.to_datetime('2021-01-10 13-30', format='%Y-%m-%d %H-%M')
    ```

    ```python
    pd.to_datetime('01102021', format='%m%d%Y')
    ```

    

  * **DatetimeIndex**

    ```python
    df.set_index('새로운열이름', inplace=True)
    ```

    * 시계열 값을 행 인덱스로 지정하면 판다스는 `DatetimeIndex`로 저장함	
    * 시간 순서에 맞춰 인덱싱 또는 슬라이싱하기 편리함

* **문자열(object)을 Period로 변환**

  ```
  df.to_period(freq='M')
  ```

  * Timestamp 객체를 일정한 기간을 나타내는 Period 객체로 변환

  * `freq` 옵션

    * 기준이 되는 기간을 설정
    * `D` : 1일의 기간
    * `M` : 1개월의 기간
    * `A` : 1년의 기간

  * 예시

    ```python
    import pandas as pd
    dates = ['2019-01-01', '2020-03-01', '2021-06-01']
    
    # 문자열 배열을 판다스 Timestamp로 변환
    ts_dates = pd.to_datetime(dates)
    
    # Timestamp를 Period로 변환
    pr_day = ts_dates.to_period(freq='D')
    pr_month = ts_dates.to_period(freq='M')
    pr_year = ts_dates.to_period(freq='A')
    ```

    ```py
    pr_day : ['2019-01-01', '2020-03-01', '2021-06-01']
    pr_month : ['2019-01', '2020-03', '2021-06']
    pr_year : ['2019', '2020', '2021']
    ```

#### 시계열 데이터 만들기

* Timestamp 배열

  ```python
  date_range(start, end, periods, freq, tz)
  ```

  * `date_range()` 
    * 여러 개의 날짜가 들어 있는 배열 형태의 시계열 데이터를 만들 수 있음
  * `start` : 시작 날짜
  * `end` : 끝 날짜. `None` 가능
  * `periods` : 생성할 Timestamp 갯수
  * `freq` : 간격
    * `M` : 월의 마지막 날짜를 생성
      * 2021-01-31, 2021-02-28, ...
    * `3M` : 3개월 간격의 마지막 날짜를 생성
      * 2021-01-31, 2021-04-30, ...
    * `MS` : 월의 시작일을 생성 
      * 2021-01-01, 2021-02-01, ...
  * `tz` : 나라 설정
    * `Asia/Seoul`

  * `closed` 
    *  `'left'` : 끝 비포함
    * 기본값 : 시작, 끝 모두 포함

* Period 배열

  ```python
  period_range(start, end, periods, freq)
  ```

  * `period_range()` 
    * 여러 개의 기간이 들어 있는 시계열 데이터를 만듬
  * `end` : 주로 `None` 사용하는 듯..
  * `periods` : 생성할 Peroid 갯수

#### 시계열 데이터 활용

* 연-월-일 날짜 데이터 분리하기

  ```python
  # 문자열타입의 oldclicktime열을 시계열타입인 Timestamp로 만든 newclicktime열
  df['newclicktime'] = pd.to_datetime(df['oldclicktime'], format='%Y%m%d%H%M')
  
  # 추출하기
  df['year'] = df['newclicktime'].dt.year
  df['month'] = df['newclicktime'].dt.month
  df['day'] = df['newclicktime'].dt.day
  df['hour'] = df['newclicktime'].dt.hour
  df['minute'] = df['newclicktime'].dt.minute
  ```

* 날짜 인덱스 활용

  ```python
  책 참고 (P212)
  ```

  

#### freq 옵션

* `D` : 1일
* `W` : 1주
* `M` : 월 말
* `MS` : 월 초
* `Q` : 분기 말
* `QS` : 분기 초
* `A` : 연 말
* `AS` : 연 초
* `B` : 휴일 제외
* `H` : 1시간
* `T` : 1분
* `S` : 1초