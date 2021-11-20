# 판다스 내장 그래프

* 시리즈 또는 데이터프레임 객체에
* `plot()` 메소드를 적용하고 `kind 옵션`으로 그래프의 종류를 선택
* 그래프를 그리다 보면 전치해야 하는 상황도 생긴다
  * `df = df.T`

#### kind 옵션

* `line` : 선그래프
* `bar` : 수직 막대 그래프
* `barh` : 가로 막대 그래프
* `his` : 히스토그램
* `box` : 박스 플롯
* `kde` : 커널 밀도 그래프
* `area` : 면적 그래프
* `pie` : 파이 그래프
* `scatter` : 산점도 그래프
* `hexbin` : 고밀도 산점도 그래프

#### 폰트 설정

```python
from matplotlib import font_manager, rc
font_path = "data/malgun.ttf"   #폰트파일의 위치
font_name = font_manager.FontProperties(fname=font_path).get_name()
rc('font', family=font_name)
df.plot()
```

#### 그래프 저장

```python
import matplotlib.pyplot as plt
box_plot = df.plot(kind='box')
plt.savefig('output/test.png')
```



---



## 선 그래프

> 별다른 옵션들을 추가하지 않으면 가장 기본적인 선 그래프를 그림

```python
df.plot()
```

* x축 : 행이름

* y축 : 열이름



---



## 막대 그래프

```python
df.plot(kind='bar')
```

* x축 : 행이름

* y축 : 열이름

* 옵션
  * `stacked=True`
    * 기본값은 False
    * 그래프를 옆으로 나열이 아닌 쌓기

---



## 히스토그램

```python
df.plot(kind='hist')
```

* x축 : 행이름

* y축 : 열이름



---



## 산점도

```python
df.plot(x='열이름1', y='열이름2', kind='scatter')
```

* 데이터프레임의 열 중에서 서로 비교할 두 변수를 선택해야 함



---



## 박스 플롯

> 특정 변수의 데이터 분포와 분산 정도에 대한 정보를 제공함

```
df[['열이름1', '열이름2']].plot(kind='box')
```

* 데이터프레임의 열 중에서 두 변수 선택



---



## 원그래프

```python
df.plot(kind='pie', y='열이름')
```

