# 한글 단어 분석



---



## 1. 한글 단어 분석을 위한 패키지 준비

```python
import json
import re

from konlpy.tag import Okt

from collections import Counter

import matplotlib
import matplotlib.pyplot as plt
from matplotlib import font_manager, rc
import wordcloud
```



---



## 2. 데이터 준비

#### 2-1 파일 읽기

```python
filename = 'etnews.kr_facebook_2016-01-01_2018-08-01_4차 산업혁명'
inputFileName = 'data/'+filename
data = json.loads(open(inputFileName+'.json', 'r', encoding='utf-8').read())
# data #출력하여 내용 확인
```

#### 2-2 분석할 데이터 추출

```python
message = ''

for item in data:
    if 'message' in item.keys(): 
        message = message + re.sub(r'[^\w]', ' ', item['message']) +''
        
message #출력하여 내용 확인
```

#### 2-3 품사 태깅 : 명사 추출

```python
nlp = Okt()
message_N = nlp.nouns(message)
message_N   #출력하여 내용 확인
```



---



## 3. 데이터 탐색

#### 3-1 단어 빈도 탐색

```python
count = Counter(message_N)

count   #출력하여 내용 확인
```

```python
word_count = dict()

for tag, counts in count.most_common(80):
    if(len(str(tag))>1):
        word_count[tag] = counts
        print("%s : %d" % (tag, counts))
```



---



## 4. 데이터 시각화

#### 4-1 히스토그램

```python
from matplotlib import font_manager, rc
font_path = "data/THEdog.ttf"   #폰트파일의 위치
font_name = font_manager.FontProperties(fname=font_path).get_name()
rc('font', family=font_name)
```

```python
plt.figure(figsize=(12,5))
plt.xlabel('키워드')
plt.ylabel('빈도수')
plt.grid(True)

sorted_Keys = sorted(word_count, key=word_count.get, reverse=True)
sorted_Values = sorted(word_count.values(), reverse=True)

plt.bar(range(len(word_count)), sorted_Values, align='center')
plt.xticks(range(len(word_count)), list(sorted_Keys), rotation='75')

plt.show()
```

```python
word_count
```

#### 4-2 워드클라우드

```python
wc = WordCloud(font_path, background_color='ivory', width=800, height=600)
cloud=wc.generate_from_frequencies(word_count)

plt.figure(figsize=(8,8))
plt.imshow(cloud)
plt.axis('off')
plt.show()
```

