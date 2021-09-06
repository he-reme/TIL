# EDA

> 탐색적 데이터 분석
>
> 음식 재료 ...
>
> `exam11`

1. 데이터에 대한 질문 , 문제 만들기
2. 데이터를 시각화하고, 변환하고, 모델링하여 그 질문, 문제에 대한 답 찾아보기
3. 찾는 과정에서 배운 것들을 토대로 다시 질문을 다듬고 또 다른 질문, 문제 만들기

* 전체적으로 데이터의 속성들을 살펴본다
  * 결측치와 이상치 체크와 처리
* 속성 간의 관계 분석한다
  * 타입, 범주형 연속형 체크, 시각화와 상관계수를 통한 상관성 체크



---



## 데이터의 결측치와 특이값(이상치) 체크와 처리

> EDA의 핵심

#### 데이터 읽어서 정보 보기

```
import pandas as pd
bank_df = pd.read_csv('data/bank.csv')
bank_df.head()
```

```python
# 데이터의 건수, 항목수를 확인
print(bank_df.shape)

# 데이터형을 확인
print(bank_df.dtypes)

# 데이터에 대한 여러가지 정보들을 한번에 출력
bank_df.info()

# 기술 통계량 확인
bank_df.describe()
```

#### 데이터 변환

* 원하는 데이터 형식으로 변환

#### 결측치 확인

```
bank_df.isna().sum() 
```

```
# 시각화로 결측치 확인 1
import seaborn as sns
sns.heatmap(bank_df.isnull(), cbar=False)
```

```
# 시각화로 결측치 확인 2
import missingno as msno 
msno.matrix(bank_df, figsize=(12,5), sparkline=False)
```

#### 결측치 삭제

* 결측치를 포함한 행 삭제

  ```python
  # job과 education 열에서 결측치가 포함된 행을 삭제
  bank_df = bank_df.dropna(subset=['job', 'education'])
  
  # 데이터의 건수, 항목수를 확인
  print(bank_df.shape)
  ```

* 결측치를 2400개 이상 포한한 열 삭제

  ```
  # 결측치이 2400개 이상인 열을 제외
  bank_df = bank_df.dropna(thresh=2400, axis=1) # axis 중요!!!
  
  # 데이터의 건수, 항목수를 확인
  print(bank_df.shape)
  print(bank_df.info())
  ```

#### 결측치 채우기

* 결측치 치환

  ```
  # 결측치을 「unknown」으로 치환
  bank_df = bank_df.fillna({'contact':'unknown'})
  ```

* 치환 외 다른 방법

  ```
  # 예시 데이터
  import numpy as np
  time_index = pd.date_range("2020-01-01", periods=5, freq="MS")
  
  dataframe = pd.DataFrame(index=time_index)
  
  dataframe["Sales"] = [1.0,2.0,np.nan,np.nan,5.0]
  dataframe
  ```

  ```
  # 1. 누락된 값을 보간 (선형보간)
  dataframe.interpolate()
  ```

  * `limit_direction` 옵션
    * `'forward'` : 앞쪽 값으로 채우기
    * `'backward'` : 뒤쪽 값으로 채우기
    * `'both'` 

  ```
  # 2. 앞쪽 값으로 채우기(Forward-fill)
  dataframe.ffill()
  dataframe.fillna(method ='ffill') 
  ```

  ```
  # 3. 뒤쪽 값으로 채우기(Back-fill)
  dataframe.bfill()
  dataframe.fillna(method ='bfill') 
  ```



---



## 범주형 데이터 전처리

> EDA 작업이후 데이터 전처리에서 필요한 작업

* 범주형 변수의 값을 수치로 변환
* 사이킷런은 문자열 값을 입력 값으로 처리 하지 않기 때문에 숫자 형으로 변환해야 함
  * 범주형 변수의 경우 : 전처리를 통해 정수값으로 변환
  * 범주형이 아닌 단순 문자열인 경우 : 일반적으로 제거
* 범주형 변수의 처리 방법
  * 레이블 인코딩
  * 더미화(원 핫 인코딩)

#### 레이블 인코딩

* 문자열(범주형) 값을 0부터 1씩 증가하는 값으로 변환

* 숫자의 차이가 모델에 영향을 주지 않는 **트리 계열 모델에 적용**

  * 의사결정나무, 랜던포레스트

* 숫자의 차이가 모델에 영향을 미치는 **선형 계열 모델에는 사용하지 않음** - 더미화로 전처리

  * 로지스틱회귀, SVM, 신경망

* 직접 레이블 인코딩 구현

  ```
  # yes를 1、no를 0으로 치환
  bank_df = bank_df.replace('yes', 1)
  bank_df = bank_df.replace('no', 0)
  ```

* `sklearn.preprocessing.LabelEncoder` 사용

  ```python
  import numpy as np
  from sklearn.preprocessing import LabelEncoder
  items = ['TV','TV','냉장고','컴퓨터','냉장고','컴퓨터', '에어콘']
  
  le = LabelEncoder() # 레이블 인코더 객체 생성
  
  le.fit(items) 
  label = le.transform(items)
  
  print(label, type(label))
  print(le.classes_) # ['TV', '냉장고', '에어콘', '컴퓨터']
  print(le.inverse_transform(label))
  ```

  * `fit()` : 어떻게 변환할 지 **학습**
  * `transform()` : 문자열을 숫자로 **변환**
  * `fit_transform()` : 학습과 변환을 한번에 처리 (`fit` + `transform`)
  * `inverse_transform()` : 숫자를 문자열로 변환
  * `classes_` : 인코딩한 클래스 조회

* `encoding_columns` 레이블 인코딩 처리

  ```python
  encoding_columns = ['workclass','education','marital-status', 'occupation','relationship','race','gender','native-country', 'income'] # 범주형
  not_encoding_columns = ['age','fnlwgt', 'education-num','capital-gain','capital-loss','hours-per-week'] # 연속형
  ```

  ```
  enc_classes = {} 
  def encoding_label_func(x):  #x: 범주형 타입의 컬럼(Series)
      le = LabelEncoder()
      label = le.fit_transform(x)
  
      enc_classes[x.name] = le.classes_   #x.name: 컬럼명
  
      return label
  ```

  ```
  d1 = df[encoding_columns].apply(encoding_label_func)
  d2 = df[not_encoding_columns]
  data = d1.join(d2)
  data.head()
  ```

#### 더미화 (원핫 인코딩)

* N개의 클래스들 N차원의 One-Hot 벡터로 표현되도록 변환

* 고유값들을 변수(피처, 열)로 만들고 정답에 해당하는 열은 1로 나머지는 0으로 표시

* 변환해야 하는 값의 종료가 여러 개일 때

* 숫자의 차이가 모델에 영향을 미치는 선형 계열 모델에서 범주형 데이터 변환시 사용

* 판다스

  * `pandas.get_dummies(DataFrame [, columns=[변환할 컬럼명]])` 함수 이용

    * 옵션
      * `dummy_na = True` 

  * DataFrame에서 범주형(문자열) 변수만 변환

  * 예시

    ```
    import pandas as pd
    df = pd.DataFrame({'item' : ['TV', '냉장고', '전자레인지', '컴퓨터', 'TV', '선풍기', '선풍기', '믹서', '믹서']})
    pd.get_dummies(df)
    pd.get_dummies(df['item'])
    ```

* 사이킷런

  * `sklearn.preprocessing.OneHotEncoder` 이용
  * `fit()` : 어떻게 변환할 지 학습
  * `transform()` : 문자열을 숫자로 변환
  * `fit_transform()` : 학습과 변환을 한번에 처리
  * `get_feature_names()` : 원핫인코딩으로 변환된 컬럼의 이름을 반환
  * DataFrame을 넣을 경우 모든 변수들을 변환하므로 범주형 컬럼만 처리하도록 해야 함



---



## 수치형 데이터 전처리

> EDA 작업 이후 데이터 전처리에서 필요한 작업

* 각 열(변수, 피처, 속성)이 가지는 값들의 숫자 범위가 다를 경우 이 값의 범위를 일정한 범위로 맞추는 작업
* 방법
  * 정규화 (Normalization)
  * 표준화 (Standardization)

#### 정규화

* **MinMax 스케일러**라고도 함

* 데이터의 상대적 크기에 대한 영향을 줄이기 위해 데이터 범위를 0~1로 변환

* 2개 이상의 대상 컬럼의 단위가 다를 때 대상 데이터를 같은 기준으로 볼수 있게 함

* 식

  * `(측정값-최소값) / (최대값-최소값)`

* **sklearn.preprocessing의 MinMaxScaler 사용**

  ```
  from sklearn.preprocessing import MinMaxScaler
  a = [[10], [9], [8], [6], [2]]
  
  scaler = MinMaxScaler(feature_range=(0,1))
  a = scaler.fit_transform(a)
  ```

#### 표준화

* **Z-score 표준화**라고도 함
* 피쳐의 값들이 평균이 0이고 표준편차가 1인 범위(표준정규분포)에 있도록 변환
* 데이터가 평균으로부터 얼마나 떨어져있는지 나타내는 값으로, 특정 범위를 벗어난 데이터는 outlier로 간주, 제거
* 특히 **SVM, 선형회귀, 로지스틱 회귀 알고리즘(선형모델)**은 데이터셋이 표준정규분포를 따를 때 성능이 좋은 모델이기 때문에, 표준화를 하면 대부분의 경우 성능이 향상됨
  * 트리계열을 제외한 대부분의 머신러닝 알고리즘들이 피처의 스케일에 영향을 받음	
* 데이터를 0을 중심으로 양쪽으로 데이터를 분포시키는 방법
* 식
  * `(측정값-평균) / 표준편차`

* **sklearn.preprocessing의 StandardScaler 사용**

  ```python
  from sklearn.preprocessing import StandardScaler
  a = [[10], [9], [8], [6], [2]]
  
  scaler = StandardScaler()
  a = scaler.fit_transform(a)
  
  print('평균 : ', a.mean())
  print('표준편차 : ', a.std())
  ```

  