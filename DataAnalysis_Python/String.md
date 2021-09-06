# 문자열



---

## 문자열 처리 메소드 목록

#### string calculation

* `len()`
* `min()`
* `max()`
* `count()`

#### string search

* `startswith()`
* `endswith()`
* `find()`
* `rfind()`
* `index()`
* `rindex()`

#### number / character

* `isalnum()`
* `isalpha()`
* `isdigit()`
* `isnumeric()`
* `isdecimal()`

#### lower / upper

* `islower()`
* `isupper()`
* `lower()`
* `upper()`
* `swapcase()`
* `istitle()`
* `title()`
* `capitalize()`

#### space / strip

* `lstrip()`
* `rstrip()`
* `strip()`
* `isspace()`
* `canter()`

#### split / join / fill

* `split()`

  * 구분자를 기준으로 문자열 나누기

  ```
  str = "web-is-free"
  str.split('-')
  ```

* `splitlines()`

* `replace()`

* `join()`

  * 구분자를 붙여 한 문자열로 만들기

  ```
  str = ['web', 'is', 'free']
  "-".join(str) # web-is-free
  ```

* `zfill()`

* `ljust()`

* `rjust()`



---



## `re.sub()`

> 문자열 대체

```python
import re
```

```
re.sub("찾을 문자", "바꿀 문자", 대상 문자열)
```

* 여러 가지 예제

  ```python
  import re
  word = "JAVA   가나다 javascript Aa 가나다 AAaAaA123 %^&* 파이썬"
  print(re.sub("A", "", word)) # A
  print(re.sub("a", "", word)) # a
  print(re.sub("Aa", "", word)) # Aa
  print(re.sub("(Aa){2}", "", word)) # AaAa (중괄호는 반복횟수)
  print(re.sub("[Aa]", "", word)) # A 또는 a
  ```

  ```python
  print(re.sub("[가-힣]", "", word)) # 한글만 삭제 
  print(re.sub("[^가-힣]", "", word)) # 한글을 제외하고 삭제
  ```

  ```python
  print(re.sub("[&^%*]", "", word))
  print(re.sub("[^가-힣A-Za-z0-9\s]", "", word))
  # 가-힣, A-Z, a-z, 0-9, 공백 모두 제외하고 삭제 (특수문자 제거)
  ```

  ```python
  print(re.sub("[\w\s]", "", word)) # 워드나 공백 삭제
  print(re.sub("\s", "", word)) # 공백 삭제
  print(re.sub("\d", "", word)) # 숫자 삭제
  print(re.sub("\D", "", word)) # 숫자가 아닌것 삭제 (대문자는 ^와 같은 의미..)
  ```

  ```python
  print(re.sub("[^\w]", "", word)) # 워드가 아닌것 삭제
  print(re.sub("\W", "", word)) # 워드가 아닌 것 삭제 (대문자는 ^와 같은 의미...)
  ```

  ```python
  new_word = re.sub("[^가-힣\s]", "", word)
  print(new_word)
  ```

  ```python
  new_word = re.sub("\s+", " ", new_word) # 연이어 나오는 공백 모두 찾아서 하나로 만들어주기
  print(new_word)
  ```

  ```python
  print(new_word.strip()) # 앞이나 뒤에 있는 공백 제거
  ```

* 데이터프레임의 모든 행에 적용

  ```
  df_new['발생년'] = df_new['발생년'].map(lambda x: re.sub('년', '', x))
  ```

  * `2016년` → `2016`
  * 람다 적용