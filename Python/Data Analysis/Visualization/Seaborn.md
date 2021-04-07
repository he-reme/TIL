# Seaborn

> 라이브러리
>
> `exam7`

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



---



## 예시

* 회귀선 그리기

```python
import matplotlib.pyplot as plt
import seaborn as sns
 
# Seaborn 제공 데이터셋 가져오기
titanic = sns.load_dataset('titanic')
 
# 스타일 테마 설정 (5가지: darkgrid, whitegrid, dark, white, ticks)
sns.set_style('darkgrid')

# 그래프 객체 생성 (figure에 2개의 서브 플롯을 생성)
fig = plt.figure(figsize=(15, 5))   
ax1 = fig.add_subplot(1, 2, 1)
ax2 = fig.add_subplot(1, 2, 2)
 
# 그래프 그리기 - 선형회귀선 표시(fit_reg=True)
sns.regplot(x='age',        #x축 변수
            y='fare',       #y축 변수
            data=titanic,   #데이터
            ax=ax1)         #axe 객체 - 1번째 그래프 

# 그래프 그리기 - 선형회귀선 미표시(fit_reg=False)
sns.regplot(x='age',        #x축 변수
            y='fare',       #y축 변수
            data=titanic,   #데이터
            ax=ax2,         #axe 객체 - 2번째 그래프        
            fit_reg=False)  #회귀선 미표시

plt.show()
```

