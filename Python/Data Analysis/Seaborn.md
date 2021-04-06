# Seaborn

> 라이브러리

#### 임포트

```python
import seaborn as sns
```



#### Seaborn 내장 데이터셋 불러오기

````
sns.load_dataset('데이터셋')
````



---



#### heatmap

```python
# 예제 6-20
# 라이브러리 불러오기
import pandas as pd
import seaborn as sns

# IPyhton 디스플레이 설정 변경 
pd.set_option('display.max_columns', 10)    # 출력할 최대 열의 개수
pd.set_option('display.max_colwidth', 20)    # 출력할 열의 너비

# titanic 데이터셋에서 age, sex 등 5개 열을 선택하여 데이터프레임 만들기
titanic = sns.load_dataset('titanic')
df = titanic.loc[:, ['age','sex', 'class', 'fare', 'survived']]
print(df.head())
print('\n')

# 행, 열, 값, 집계에 사용할 열을 1개씩 지정 - 평균 집계
pdf1 = pd.pivot_table(
	df,               # 피벗할 데이터프레임
    index='class',    # 행 위치에 들어갈 열
    columns='sex',    # 열 위치에 들어갈 열
    values='age',     # 데이터로 사용할 열
    aggfunc='mean'	  # 데이터 집계 함수
)

print(pdf1.head())
print('\n')
```

```python
sns.heatmap(pdf1, annot=True)
```

* 피벗 테이블에 대한 그래프
* `annot=True`
  * 값 표시