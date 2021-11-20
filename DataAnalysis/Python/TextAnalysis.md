# 텍스트 분석

> 자연어 처리
>
> `exam10`

#### 목차

1. KoNLPy를 활용한 형태소 분석
2. 워드 클라우드
3. nltk - 한국어 기반의 자연어 처리 모듈

4. 텍스트 전처리
5. 카운트 기반의 단어 표현
6. 한글 자모 분해와 결합



---



## KoNLPy를 활용한 형태소 분석

> KoNLPy : 한국어 정보처리를 위한 파이썬 패키지

#### `Kkma`

```python
from konlpy.tag import Kkma
from konlpy.utils import pprint
import pandas as pd
import numpy as np 
```

* `kkma` 객체 생성

  ```python
  kkma = Kkma()
  ```

* 문장 나누기

  ```python
  pprint(kkma.sentences('네, 안녕하세요. 반갑습니다.'))
  ```

* 명사 추출

  ```python
  pprint(kkma.nouns('질문이나 건의사항은 깃헙 이슈 트래커에 남겨주세요.'))
  ```

* 품사 분석

  ```python
  pprint(kkma.pos('오류보고는 실행환경, 에러메세지와함께 설명을 최대한상세히!^^'))
  ```

#### 형태소 분석기 종류

* 분석기 여러개 있음. 분석기마다 조금씩 분석하는게 다름

* 상황에 따라 원하는 것 사용하기

  ```python
  from konlpy.tag imort 원하는형태소분석기이름
  ```
  * Kkma
  * Hannanum
  * Okt : 요즘 이거 많이 사용하는 듯
  * Komoran

#### 메소드

* 객체 생성

  ```python
  형태소분석기객체 = 형태소분석기이름()
  ```

* 문장 나누기

  ```python
  형태소분석기객체.sentences('문자열')
  ```

* 명사 추출

  ```python
  형태소분석기객체.nouns('문자열')
  ```

* 단어 나누기

  ```python
  형태소분석기객체.morphs('문자열')
  ```

* 품사 분석

  ```python
  형태소분석기객체.pos('문자열')
  ```

* 태그셋 확인

  ```python
  형태소분석기객체.tagset
  ```



---



## 워드 클라우드

#### 기본

```python
from wordcloud import WordCloud
import matplotlib.pyplot as plt 
```

* 워드클라우드 객체 생성

  ```python
  myfontpath = "data/THEdog.ttf" # 폰트 설정
  wc = WordCloud(
      font_path = myfontpath,
      background_color = 'white'
      width = 200,
      height = 200
  )
  ```

* generate 및 워드클라우드 이미지 생성

  * 명사 리스트로 워드 클라우드 생성

    ```python
    text = "둘리 도우너 또치 마이콜 희동이 둘리 둘리 도우너 또치 토토로 둘리 올라프 토토로 올라프 올라프"
    wc = wc.generate(text)   
    ```

  * 빈도별로 워드 클라우드 생성

    ```python
    keywords = {'파이썬':7, '넘파이':3, '판다스':5, '매트플롭립':2, '시본':2, '폴리엄':2}             ## 특정 단어의 빈도를 딕셔너리로 만든다 
    
    wc = wc.generate_from_frequencies(keywords)
    ```

* 생성한 워드 클라우드 jupyter lab에서 바로 확인하기

  ```python
  fig = plt.figure()
  plt.imshow(wc, interpolation='bilinear')
  plt.axis('off') # 좌표 없애기
  plt.show()
  ```

* 워드클라우드 이미지로 저장

  ```python
  wc.to_file('output/test.png')
  ```

#### 이미지 모양대로 워드 클라우드 생성

```python
from PIL import Image # 이미지 파일 처리하는 모듈 
import numpy as np
from wordcloud import STOPWORDS  
```

* 이미지를 읽어와서 다차원 배열로 변환

  ```python
  # 테스트 이미지는 로봇 이미지 (배경이 투명인 이미지여야 함)
  r2d2_mask = np.array(Image.open('data/r2d2.JPG')) 
  ```

* 한글은 별도 집합으로 불용어를 만듬

  ```python
  stopwords = set()
  stopwords.add("은")
  stopwords.add("입니다")
  stopwords.add("것인가")
  stopwords.add("처럼")
  ```

* 워드 클라우드 객체 생성

  ```python
  wc = WordCloud( 
  	stopwords=stopwords, # 불용어           
      font_path = myfontpath,
      background_color='white',
      width = 800,
      height = 800,
      mask=r2d2_mask # 마스크 인자에 이미지 전달
  )
  ```

* generate

  ```python
  texts = ['로봇 처럼 표시하는 것을 보기 위해 이것 은 예문 입니다 가을이라 겨울 바람 솔솔 불어오니 ', '여러분 의 문장을 넣 으세요 ㅎㅎㅎ 스타워즈 영화에 나오는 다양한 로봇처럼 r2d2']
           
  # 두 개의 문자을 연결해서 워드클라우드를 만든다 
  wc = wc.generate_from_text(texts[0]+texts[1]) 
  wc
  ```

* 확인하기

  ```python
  plt.figure(figsize=(8,8))
  plt.imshow(wc, interpolation="bilinear") # 이미지를 출력하면 전달된 모양에 따라 표시됨
  plt.axis("off")
  plt.show()
  ```

#### 불용어 만들기

* 불용어 객체 생성

  ```python
  stopwords = set()
  ```

* 불용어 추가

  ```python
  stopwords.add("은")
  ```

* 워드 클라우드에 적용

  ```python
  wc = WordCloud( 
  	stopwords=stopwords, # 인자 추가         
      font_path = myfontpath,
      background_color='white',
      colormap = 'coolwarm', # 텍스트 칼라 지정
      width = 800,
      height = 800,
  )
  ```



---



## nltk

> 한국어 기반의 자연어 처리 모듈
>
> Natural Language Toolkit

```python
import nltk
```

```python
# 테스트할 수 있는 텍스트 데이터셋 
from konlpy.corpus import kobill
files_ko = kobill.fileids()
files_ko # 데이터셋 리스트 확인
```

```python
# 특정 텍스트 파일을 읽기
doc_ko = kobill.open('1809898.txt').read()
```

* 텍스트에서 명사 추출

  ```python
  from konlpy.tag import Okt      
  t = Okt()
  tokens_ko = t.nouns(doc_ko) # 텍스트에서 명사를 추출한다. 
  print(tokens_ko[:10])
  ```

* 명사로 추출한 것을 텍스트 객체로 만듬

  ```python
  nouns_text = nltk.Text(tokens_ko, name='국군부대의 소말리아 해역 파견연장 동의안')
  ```

#### 사용하기 

* 명사로 분리된 개수를 확인

  ```python
  len(nouns_text.tokens)
  ```

* 유일한 단어의 개수 확인

  ```python
  len(set(nouns_text.tokens))
  ```

* 동일한 단어의 발생 빈도 확인

  ```python
  nouns_text.vocab()
  ```

* 특정 단어의 발생빈도 확인

  ```python
  nouns_text.count('파견')
  ```

* 특정 단어가 있는 곳 리턴

  ```python
  nouns_text.concordance('소말리아')
  ```

* 가장 많이 발생한 단어 순으로 (단어, 빈도수) 리스트에 담음. 

  ```
  data = nouns_text.vocab().most_common(표시하고싶은갯수)
  ```

#### 워드클라우드 생성

```python
# 단어별 빈도수를 딕셔너리로 변환해서 전달한다 
wc = WordCloud(
	font_path=myfontpath,                     
    relative_scaling = 0.2,
    background_color='white',  
).generate_from_frequencies(dict(data))
    
plt.figure(figsize=(10,6))
plt.imshow(wc)
plt.axis("off")                                           plt.show()
```



---



## 텍스트 전처리

#### 한국어 전처리 패키지

* PyKoSpacing
  * 한국어 띄어쓰기 패키지
  * 띄어쓰기가 되어있지 않은 문장을 띄어쓰기한 문장으로 변환해주는 패키지
  * 대용량 코퍼스를 학습하여 만들어진 띄어쓰기 딥러닝 모델로 준수한 성능을 가짐
* Py-Hanspell
  * 맞춤법 검사 및 띄어쓰기
  * 띄어쓰기 검사는 PyKoSpacing이 더 나은듯!

#### PyKoSpacing

```python
from pykospacing import spacing
```

```python
sent = '김철수는 극중 두 인격의 사나이 이광수 역을 맡았다. 철수는 한국 유일의 태권도 전승자를 가리는 결전의 날을 앞두고 10년간 함께 훈련한 사형인 유연재(김광수 분)를 찾으러 속세로 내려온 인물이다.'

# 띄어쓰기가 없는 문장 임의로 만들기
new_sent = sent.replace(" ", '')
```

```python
# 띄어쓰기 적용
kospacing_sent = spacing(new_sent)
```

#### Py-Hanspell

```python
from hanspell import spell_checker
```

```python
sent = "맞춤법 틀리면 외 않되? 쓰고싶은대로쓰면돼지 "
spelled_sent = spell_checker.check(sent)

# 맞춤법 적용
hanspell_sent = spelled_sent.checked
print(hanspell_sent)
```



---



## 카운트 기반의 단어 표현

> 빈도수가 클수록 중요도 낮음, 빈도수가 작을수록 중요도 높음 표현

#### 토큰화

>  토큰화 : 주어진 코퍼스(corpus)에서토큰(token)이라 불리는 단위로 나누는 작업을 토큰화라고 함

* 방법1 - nltk 패키지의 `word_tokenize()` 사용

  ```python
  import nltk
  nltk.download('punkt')
  ```

  ```python
  from nltk.tokenize import word_tokenize 
  
  corpus = "고기를 아무렇게나 구우려고 하면 안 돼. 고기라고 다 같은 게 아니거든. 예컨대 삼겹살을 구울 때는 중요한 게 있지."
  
  word_tokens1 = word_tokenize(corpus)
  print(word_tokens1) 
  ```

* 방법2 - Okt 객체의 `morphs()` 사용

  ```python
  from konlpy.tag import Okt
  
  corpus = "고기를 아무렇게나 구우려고 하면 안 돼. 고기라고 다 같은 게 아니거든. 예컨대 삼겹살을 구울 때는 중요한 게 있지."  
  
  t = Okt()  
  word_tokens2 = t.morphs(corpus)  
  print(word_token2)
  ```

* 방법3 - Okt 객체의 `nouns()` 사용

  ```python
  from konlpy.tag import Okt
  
  corpus = "고기를 아무렇게나 구우려고 하면 안 돼. 고기라고 다 같은 게 아니거든. 예컨대 삼겹살을 구울 때는 중요한 게 있지."  
  
  t = Okt() 
  word_tokens3 = t.nouns(corpus)  
  print(word_tokens3)
  ```

* stop_words를 지정하고, 이를 제외한 토큰 출력

  ```python
  stop_words = "아무거나 아무렇게나 어찌하든지 같다 비슷하다 예컨대 이럴정도로 하면 아니거든 게 때"
  stop_words = stop_words.split(' ')
  
  result = [] 
  for w in word_tokens1: 
      if w not in stop_words: 
          result.append(w) 
  
  print(result)
  ```

#### 카운트 기반의 단어 표현

* Bag of Words
  * 단어의 순서는 고려하지 않고, 단어들의 출현 빈도에만 집중하는 텍스트 데이터의 수치화 표현 방법
* DTM (도는 TDM)
  * BoW의 확장으로서 TF 방법과 TF-IDF 방식으로 생성 가능
    * TF-IDF : 빈도수 기반 단어 표현에 단어의 중요도에 따른 가중치를 주는 방법
* 사이킷 런 (sklearn)
  * CountVectorizer 클래스 지원
  * CountVectorizer  : 단어의 빈도를 Count하여 Vector로 만드는 클래스

* 사용 예시1

  ```python
  from sklearn.feature_extraction.text import CountVectorizer
  
  corpus = ["정부가 발표하는 물가상승률과 소비자가 느끼는 물가상승률은 다르다"]
  
  vector = CountVectorizer(stop_words=["정부가", "소비자가"])
  r = vector.fit_transform(corpus).toarray()
  
  print(r) # 코퍼스로부터 각 단어의 빈도 수를 기록한다.
  print(r.shape)
  print(vector.vocabulary_) # 리스트 r에 대한.. {'단어':index, ...}
  ```

* 사용 예시2

  ```python
  from sklearn.feature_extraction.text import CountVectorizer
  import pandas as pd # 데이터프레임 사용을 위해
  ```

  ```python
  corpus = [
    '먹고 싶은 사과',
    '먹고 싶은 바나나',
    '길고 노란 바나나 바나나',
    '저는 과일이 좋아요'
  ] 
  ```

  ```python
  vector = CountVectorizer()
  dtm = vector.fit_transform(corpus).toarray()
  print(dtm) 
  print(vector.vocabulary_) # 각 단어들의 인덱스가 어떻게 부여되었는지를 보여준다.
  tfidf = pd.DataFrame(dtm, columns = vector.get_feature_names())
  display(tfidf)
  ```

* 사용 예시3

  ```python
  from sklearn.feature_extraction.text import TfidfVectorizer
  vector = TfidfVectorizer()
  dtm = vector.fit_transform(corpus).toarray()
  print(dtm) 
  print(vector.vocabulary_) # 각 단어들의 인덱스가 어떻게 부여되었는지를 보여줌
  tfidf = pd.DataFrame(dtm, columns = vector.get_feature_names())
  display(tfidf)
  ```

* 사용 예시4

  ```python
  corpus = [
             "커피 파스타 치킨 샐러드 아이스크림",
             "커피 우동 소고기김밥 귤",
             "참치김밥 커피 오뎅",
             "샐러드 피자 파스타 콜라",
             "티라무슈 햄버거 콜라",
             "파스타 샐러드 커피"    
  ]
  vector = CountVectorizer()
  dtm = vector.fit_transform(corpus).toarray()
  print(dtm) 
  tf = pd.DataFrame(dtm, columns = vector.get_feature_names())
  display(tf)
  
  com = dtm.T @ dtm  # 동시 출현횟수
  
  comdf = pd.DataFrame(com, columns = vector.get_feature_names(), index = vector.get_feature_names())
  display(comdf)
  ```

  

---



## 한글 자모 분해와 결합

> 한글의 자음과 모음을 분리

```
import hgtk
```

* 분해

  ```python
  hgtk.letter.decompose('문자')
  hgtk.text.decompose('문자열')
  ```

* 합침

  ```
  hgtk.letter.compose(분리된 문자들)
  hgtk.text.compose(분리된 문자들)
  ```

* 한글 여부 확인

  ```python
  hgtk.check.is_hangul('문자열')
  ```
  * True : 한글
  * False : 한글X 
  * 영어가 일부 들어가면 한글로 인식하지 않음

* 한자 여부 확인

  ```python
  hgtk.check.is_hanja('문자열')
  ```

* 단어에 맞는 조사 붙이기 

  ```
  hgtk.josa.attach('단어', hgtk.josa.EUN_NEUN) # 은/는     hgtk.josa.attach('단어', hgtk.josa.I_GA) # 이/가
  hgtk.josa.attach('단어', hgtk.josa.EUL_REUL) # 을/를
  ```

  

---



## 예시



#### 1. 명사 추출, 워드클라우드 처리, 이미지파일에 저장

```python
import re

f = open("C:/KHR/PYDATAexam/data/naverhotel.txt", "rt", encoding="UTF-8")   
text = f.read()
text = re.sub("[^가-힣\s]", "", text)
f.close()
```

```python
from konlpy.tag import Okt 
import nltk

okt = Okt()
nouns_list = okt.nouns(text)
nouns_text = nltk.Text(nouns_list, name='네이버 호텔')
data = data = nouns_text.vocab().most_common(150)
```

```python
from wordcloud import WordCloud
import matplotlib.pyplot as plt 

myfontpath = "C:/KHR/PYDATAexam/data/THEdog.ttf"
wc = WordCloud(
    font_path=myfontpath,                     
    relative_scaling = 0.2,
    background_color='white',
    colormap = 'plasma',
    width = 700,
    height = 500,
).generate_from_frequencies(dict(data))
    
plt.figure(figsize=(10,6))
plt.imshow(wc)
plt.axis("off")                                           
plt.show()

wc.to_file('test.png')
```

