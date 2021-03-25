# BeautifulSoup

> HTML 및 XML 파일에서 데이터를 추출하기 위한 파이썬 라이브러리
>
> urllib나 request 패키지를 통해 얻은 HTML을 분석하는 라이브러리

* 파이썬에서 기본적으로 제공하는 라이브러리 X

* Anaconda에서 BeautifulSoup 패키지가 Site-Packages로 설치되어있음

  * Anaconda prompt창에서 설치

    ```shell
    conda install bs4 #BeautifulSoup
    conda install lxml
    conda install html5lib
    ```

* 파서
  * 구문 분석기
  * HTML 및 XML 파일의 내용을 읽을 때 사용

#### 임포트

```python
import requests
from bs4 import BeautifulSoup
```

#### 파서 종류

* `html.parser`
* `lxml`
* `lxml-xml`
* `html5lib`

* 파이썬이 내장하고 있는 파서 사용해도 되고, 좀 더 성능이 좋은 파서를 추가로 설치해서 사용해도 됨



---



## HTML 파싱

1. BeautifulSoup의 메인 API인 bs4모듈에서 `BeautifulSoup()` 함수 임포트
2. 파싱할 HTML 문서와 파싱에 사용할 파서를 지정하여 호출하면, `bs4.BeautifulSoup` 객체 리턴
3. HTML 문서에 대한 파싱이 끝나면 트리 구조 형식으로 DOM 객체들이 생성되며, `bs4.BeautifulSoup` 객체를 통해 접근 가능

```python
from bs4 import BeautifulSoup
bs = BeautifulSoup(html_doc, 'html.parser')
bs = BeautifulSoup(html_doc, 'lxml')
bs = BeautifulSoup(html_doc, 'lxml.xml')
bs = BeautifulSoup(html_doc, 'html5lib')
```

* `bs`가 아닌 `bs.pretify()` 로 출력하면 들여쓰기 적용돼서 
  * 문서 내용을 이쁘게 출력함

---



## `bs4.BeautifulSoup` 객체의 태그 접근 방법

* HTML 문서를 파싱하고 `bs4.BeautifulSoup` 객체 생성

  ```python
  bs = Beautifulsoup(html_doc, 'html.parser')
  ```

* 방법1

  * `<html>`, `<head>`, `<body>` 태그는 제외하고 접근하려는 태그에 **계층 구조**를 적용하여 태그명을 `.` 연산자와 함께 사용

    ```
    bs.태그명
    bs.태그명.태그명
    bs.태그명.태그명.태그명
    ```

* 방법2
  
  * 메서드로 접근



---



## 트리구조로 태그 접근

#### 태그명 추출

```python
bs.태그명.name
```

#### 속성 추출

```
bs.태그명['속성명']
bs.태그명.attrs
```

#### 콘텐츠 추출

```python
bs.태그명.string # 자손 태그는 안꺼냄
bs.태그명.text # 자손 태그들 것 까지 모두 꺼내줌
bs.태그명.contents # 리스트 형태로 반환
bs.태그명.strings
bs.태그명.stripped_strings
```

```python
bs.태그명.string.strip() # 공백 제거
bs.태그명.text.strip()
bs.태그명.get_text()
bs.태그명.get_text(strip=True)
```

#### 부모 태그 추출

```python
bs.태그명.parent
```

#### 자식 태그들 추출

```
bs.태그명.children
```

#### 형재 태그 추출

```python
bs.태그명.next_sibling
bs.태그명.previous_sibling
bs.태그명.next_siblings
bs.태그명.previous_siblings
```

#### 자손 태그들 추출

```python
bs.태그명.descendants
```



---



## 메서드로 태그 접근

#### 주요 메서드

* `find_all()`
* `find()`
* `select()`

#### 태그 찾기 기능의 기타 메서드

* `find_parents()` / `find_parent()`
* `find_next_siblings()` / `find_next_sibling()`
* `find_previous_siblings()` / `find_previous_sibling`
* `find_all_next()` / `find_next()`
* `first_all_previous()` / `first_previous()`

#### `bs.find_all()`

```python
find_all(name=None, attrs={}, recursive=True, text=None, limit=None, **kwargs)
# name : 태그명, 정규표현식을 적용한 태그명, 태그명 리스트, 속성 정보, 함수, 논리값
# attrs : 딕셔너리 형태로 넘기게 해줌
# recursive : 자손 찾을지 말지. True(기본값) 찾기, False 찾지 않기
# text
# limit : 찾을 갯수 제한
```

* 주어진 기준에 맞는 모든 태그들을 찾아오며 결과는 `bs4.element.ResultSet` 객체로 리턴

* 정규 표현식 사용하고 싶으면
  
* `import re`
  * `re.compile()`의 리턴 값으로 넘겨줘야 함
  
* 예시

  ```python
  find_all('div') # div태그를 찿아라
  find_all(['p', 'img']) # p태그, img태그를 찾아라
  find_all(re.compile('^b')) # b로 시작하는 태그를 찾아라
  find_all(True) # 모든 태그를 찾아라
  find_all(id='link2') # id가 link2인 태그를 찾아라
  find_all(id=re.compile("para$")) # id가 para로 끝나는 태그를 찾아라
  find_all(id=True) # id속성이 있는 모든 태그들을 찾아라
  find_all('a', class_='sister') # a태그를 찾고 class속성이 sister인 태그를 찾아라
  find_all(src=re.compile("png$"), id='link1') # id가 link1인 태그를 찾고, src속성이 png로 끝나는 태그를 찾아라 
  ```

  ```python
  find_all(attrs={'src': re.compile('png$'), 'id': 'link1'})
  find_all(attrs={'align': 'right', 'class':'c1'})
  
  # 요즘은 text가 아닌 string으로 바뀜. 근데 text로 사용해도 무관
  find_all(text='example') 
  find_all(text=re.compile('example'))
  find_all(text=re.compile('^test'))
  find_all(text=['example', 'test'])
  fild_all('a', text='python')
  
  find_all('a', limit=2) # 앞에서부터 2개 까지만 찾기
  find_all('p', recursive=False) # 자손은 안찾고 싶으면 False. 기본값은 True
  ```

* 뽑은 태그들 하나씩 접근하기

  ```python
  tags = bs.find_all(...)
  for tag in tags:
  	# tag
  ```

#### `bs.find()`

```python
find(name=None, attrs={}, attrs={}, recursive=True, text=None, **kwargs)
```

* 주어진 기준에 맞는 태그 한개를 찾아오며 결과는 `bs4.element.Tag` 객체로 리턴, 결과값이 없으면 `None`을 리턴

* `find_all()`에 `limit=1`로 설정한 것과 동일하게 수행

* 예시

  ```python
  find('div') == find_all('div', limit=1)
  ```

#### `bs.select()`

```python
select(selector, namespaces=None, limit=None, **kwargs)
```

* 주어진 CSS 선택자에 맞는 태그들을 찾아오며 결과는 `list` 객체로 리턴

* CSS 선택자를 적용한 호출

  ```python
  select('태그명')
  select('.클래스명')
  select('#아이디명')
  select('태그명.클래스명')
  ```

* HTML 문서의 트리 구조를 적용한 태그 찾기

  ```python
  select('상위태그명 > 자식태그명 > 손자태그명')
  select('상위태그명.클래스명 > 자식태그명.클래스명')
  select('상위태그명.클래스명 > 자식태그명')
  select('상위태그명 > 자식태그명.클래스명')
  
  select('#아이디명 > 태그명.클래스명')
  select('태그명[속성]')
  select('태그명[속성=값]')
  select('태그명[속성$=값]')
  select('태그명[속성^=값]')
  select('태그명:nth-of-type(3)')
  ```

  

