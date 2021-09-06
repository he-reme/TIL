# Matplotlib

>  기본 그래프 도구
>
> `exam7` 와 `파이썬 머신러닝 판다스 데이터 분석` 책 참고

#### 임포트

```python
import pandas as pd
import matplotlib.pyplot as plt
import matplotlib
# %matplotlib inline
# %config InlineBackend.figure_format='reting'
```

* `pandas`
  *  그래프를 그릴 때 시리즈나 데이터프레임 객체를 사용하기 때문에 거의 같이 import 함
* `%matplotlib inline`
  * 현재 셀 바로 아래에 그래프를 그리라는 매직 명령
  * jupyter lab은 기본값으로 설정되어 있어서 굳이 수행시키지 않아도 됨
* `%config InlineBackend.figure_format='reting'`
  * 해상도가 좋은 그래프 그리기 위한 매직 명령
  * jupyter lab에서는 수행 시켜도 차이가 그닥 없음.
* `plot` 도움 문서
  * `?plt.plot`

#### 종류

* 선그래프 (기본 그래프)
* 면적 그래프
* 막대 그래프
* 히스토그램
* 산점도
* 파이 차트
* 박스 플롯



---



## 폰트 설정

> matplotlib이 사용하는 기본폰트는 한글폰트를 가지고 있지 않음
>
> 한글 폰트를 등록해주어야 함

* 전역적 방법

  ```python
  from matplotlib import font_manager, rc
  font_path = "data/malgun.ttf"   #폰트파일의 위치
  font_name = font_manager.FontProperties(fname=font_path).get_name()
  rc('font', family=font_name)
  ```

  

---



## 그래프

```python
plot([x], y, [format], data=None, *kwargs)
plot([x], y, [format1], [x2], y2, [format2], ... , **kwargs)
```

* `format` : `[marker][line][color]`

* 사용

  ```python
  plot(x, y)
  plot(x, y, 'bo') # 파란 원 마커
  plot(y) # x는 0부터 인덱싱
  plot(y, 'r+') # 빨간색 + 마커
  ```

  



---



## 그래프 그리기

> `plot`

* 데이터 준비

  ```python
  s = pd.Series(
      [5, 4, 7, 1, 12],
      index = ["둘리", "또치", "도우너", "희동이", "마이콜"]
  )
  ```

* 그래프 크기 설정

  ```python
  plt.figure(figsize=(10,6)) # 기본 6,4
  ```

  * 기본값 : `(6,4)`
  * 단위 : inch
  * 그래프 그릴 때 크기 설정하고 싶으면 **가장 먼저 코드 써줘야 함**

* 그래프 제목 설정

  ```python
  title_font = {
      'fontsize': 16,
      'fontweight': 'bold'
  }
  plt.title('그래프 제목', fontdict=title_font, loc='right') # loc은 위치
  ```

* label 이름 설정

  ```python
  plt.ylabel('y축 이름')
  plt.xlabel('x축 이름')
  ```

* label 설정

  ```python
  ax = plt.gca()
  ax.tick_params(axis='x', colors='blue')
  ax.tick_params(axis='y', colors='red')
  ```

* 그래프 그리기

  ```python
  plt.plot(...) #1
  plt.bar(...) #2
  df.plot(kind='bar', ...) #3
  ```

* x축, y축 범위 지정

  ```python
  plt.xticks([0, 1, 2])
  plt.yticks(range(1, 6))
  ```

  ```python
  plt.xticks([0, 1, 2], labels=['혜림', '정섭', '부모님'])
  plt.yticks(range(1, 8), ['sun', 'mon', ... , 'fri', 'sat'])
  ```

* 그래프 저장

  ```python
  plt.savefig("test.png") 
  ```

  * 반드시 `plt.show()` 이전에 코드를 써줘야 함

* 그래프 배경에 그리드 그리기

  ```python
  plt.grid()
  ```

* 그래프 배경에 보조선 추가하기

  ```python
  plt.axhline(1, 0, 0.55, color='gray', linestyle='--', linewidth='1') # 수평선
  plt.axvline(1, 0, 0.16, color='gray', linestyle=':', linewidth='1') # 수직선
  
  ```

* 한 도화지 위에 여러 그래프 그리고 싶을 때 어떤 그래프인지 알려주는 legend

  ```python
  plt.legend(['y1', 'y2', 'y3'])
  ```

* 그래프 보기

  ```python
  plt.show()
  ```

  

---



## 선 그래프

```python
plt.plot(x, y, '선종류')
```

* 선종류

  * 선 모양, 색
  * 예
    * `r--`
    * `gv-`
    * `m-.`

* 한 그래프 위에 여러 선을 그리고 싶으면

  * 방법1

    ```python
    plt.plot(x1, y1, '종류1', x2, y2, '종류2', x3, y3, '종류3', ...)
    plt.show()
    ```

  * 방법2

    ```python
    plt.plot(x1, y1, '종류1')
    plt.plot(x2, y2, '종류2')
    plt.plot(x3, y3, '종류3')
    plt.show()
    ```

    * `plt.show()` 하기 전까지 해당 선들을 한 그래프 위에 그림

  * 어떤 선이 어떤 선인지 알려주는 `legend`

    ```python
    plt.legend(["y1", "y2", "y3"])
    ```

    * 예시

      ```python
      plt.grid(True, axis='y', color='red', alpha=0.5, linestyle='--')
      ```

      * 가로선만 그려짐





---



## 막대 그래프

```python
plt.bar(x, height, width=0.8, bottom=None,*, align='center', data=None, **kwargs)
```



---



## 산점도

```python
import numpy as np
from matplotlib import pyplot as plt
t = np.array([0,1,2,3,4,5,6,7,8,9])
y = np.array([9,8,7,9,8,3,2,4,3,4])
```

```python
plt.figure(figsize=(10,6))
plt.scatter(t,y, s = 50, c = t, marker='>')
plt.colorbar()
plt.show()
```



---



## 원그래프

* 그림자 + 띄어있는 원 그래프

  ```python
  explode = [0.05, 0.05, 0.05, 0.05]
  colors = ['#ff9999', '#ffc000', '#8fd9b6', '#d395d0']
  
  plt.figure(figsize=(10,6))
  plt.pie(df.sum(), labels=df.columns, autopct='%.1f%%',
          explode=explode, colors=colors, shadow=True)
  plt.savefig("hw3.png")
  plt.show()
  ```

* `lamda` 사용

  ```python
  plt.figure(figsize=(10,6))
  colors = ['#ff9999', '#ffc000', '#8fd9b6', 'lightgray', '#d395d0', 'whitesmoke']
  
  plt.pie(df.T.sum(), labels=df.T.columns.map(lambda x : str(x)+'년'), 
          autopct='%.1f%%', colors=colors)
  plt.savefig("hw4.png")
  plt.show()
  ```



---



## 박스 플롯

```python
import numpy as np
from matplotlib import pyplot as plt
s1 = np.random.normal(loc=0, scale=1, size=1000) # 평균 0 표준편차 1
s2 = np.random.normal(loc=5, scale=0.5, size=1000) # 평균 5 표준편차 0.5
s3 = np.random.normal(loc=10, scale=2, size=1000) # 평균 10 표준편차 2
```

```python
plt.figure(figsize=(10,6))
plt.boxplot((s1, s2, s3), labels=['월요일', '수요일', '금요일'])
plt.grid()
plt.show()
```



---



## 한 도화지에 여러 그래프 그리기

```python
plit.subplot(행, 열, 몇번째 행)
```

* 위 아래로 2개 그래프 그리기

  ```python
  plt.figure(figsize=(10,8))
  
  plt.subplot(2,1,1)
  plt.title('matplotliab 그래프(1)')
  plt.plot([1,2,3,4,5,6],[10,3,7,4,6,3])
  
  plt.subplots_adjust(hspace=1) # 그래프 사이에 공간 주기
  
  plt.subplot(2,1,2)
  plt.title('matplotliab 그래프(2)')
  plt.plot([1,2,3,4,5,6],[10,3,7,4,6,3], 'r--', lw=7)
  
  plt.show()
  ```

* 좌 우로 2개 그래프 그리기

  ```python
  plt.subplot(1,2,1)
  plt.title('matplotliab 그래프(3)')
  plt.plot([1,2,3,4,5,6],[10,3,7,4,6,3], 'yp-.')
  
  plt.subplot(1,2,2)
  plt.title('matplotliab 그래프(4)')
  plt.plot([1,2,3,4,5,6],[10,3,7,4,6,3], 'r:', lw=7)
  
  plt.show()
  ```

* 2 X 2 로 나눠서 그리기

  ```python
  plt.figure(figsize=(10,6))
  
  plt.subplot(2,2,1) # plt.subplot(221)과 같은 의미
  plt.subplot(2,2,2)
  plt.subplot(2,2,3)
  plt.subplot(2,2,4)
  
  plt.show()
  ```

* 위에 2개, 아래 1개 그리기

  ```
  plt.figure(figsize=(10,6))
  
  plt.subplot(2,2,1)
  plt.subplot(2,2,2)
  plt.subplot(2,1,2)
  
  plt.show()
  ```

* 다른 방법

  ```python
  import numpy as np
  import matplotlib.pyplot as plt
  
  # data
  x=np.linspace(-3,3,100)
  y1=np.sin(x)
  y2=np.cos(x)
  y3=1/(1+np.exp(-x))
  y4=np.exp(x)
  
  # 그래프 그리기
  fig, ax = plt.subplots(2, 2)
  
  ax[0, 0].plot(x, y1)
  ax[0, 1].plot(x, y2)
  ax[1, 0].plot(x, y3)
  ax[1, 1].plot(x,y4)
  
  ax[0, 0].set_title("Sine function")
  ax[0, 1].set_title("Cosine function")
  ax[1, 0].set_title("Sigmoid function")
  ax[1, 1].set_title("Exponential function")
  
  plt.show()
  ```

  

---



## 칼라맵

* matplotlib에서 제공하는 칼라맵 리스트 확인

  ```python
  plt.cm.datad.keys()
  ```

* seaborn의 `color_palette()` 함수로 칼라 확인할 수 있음

  ```python
  import seaborn as sns
  sns.color_palette('matplotlib칼라맵', 갯수)
  ```

  ```python
  sns.color_palette('Pastel1', 10)
  ```

#### 예시1

```python
import matplotlib.pyplot as plt
import matplotlib
import seaborn as sns

data_result = pd.read_csv("./data/cctv_seoul.csv")
display( data_result.head(3))

data_result.set_index('구별', inplace=True)
data_result.head()

mycolors = sns.color_palette('hls',len(data_result['CCTV수']))

plt.figure(figsize=(10,10))
data_result['CCTV수'].plot(kind='barh', grid=True, color=mycolors)
plt.xlabel('각 구에 설치된 CCTV 댓수', size=15)
plt.ylabel('구이름', size=15)
plt.title('구별 CCTV 설치 현황(1)', size=20)

plt.savefig("output/hw1.png") 
plt.show()
```

#### 예시2

```
import pandas as pd
from matplotlib import font_manager, rc

font_path = "C:/KHR/PYDATAexam/data/malgun.ttf"   #폰트파일의 위치
font_name = font_manager.FontProperties(fname=font_path).get_name()
rc('font', family=font_name)

df = pd.read_csv("C:/KHR/PYDATAexam/data/product_click.log", sep=' ', header=None)
df.columns = ['클릭날짜', '상품ID']
```

```python
import matplotlib.pyplot as plt
import matplotlib
import seaborn as sns

ID_group = df.groupby('상품ID')
productID = []
clickCount = []
for key, group in ID_group :
    productID.append(key)
    clickCount.append(len(group))
    
df_click = pd.DataFrame({'상품ID':productID, '클릭횟수':clickCount})
df_click.sort_values(by='클릭횟수', ascending=False, inplace=True)

mycolors = sns.color_palette('Pastel1',len(df_click['클릭횟수']))
plt.figure(figsize=(10,7))
df_click['클릭횟수'].plot(kind='bar', grid=True, color=mycolors )
plt.xlabel('상품 ID', size=15)
plt.ylabel('클릭횟수', size=15)
plt.title('상품별 클릭 횟수', size=20)
```

