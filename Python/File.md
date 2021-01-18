# File

```python
f = open("test.txt", "wt", encoding="UTF-8")
f.write("""화이팅!
힘들어도
포기하지말자""")
f.close()
```



---



## `open`

> 파일 열기
>
> default 인코딩 값 : `cp949`

####  `open` 모드

* `wt` : write text mode
* `rt` : read text mode

* `at` : append text mode
  * 기존 내용을 그대로 두고 새로운 문자를 추가
  * `rt`와 동일하게 그냥 `f.wirte()` 사용해서 추가하면 됨.

#### (1) `open`

```python
f = open("test.txt", "wt", encoding="UTF-8")   
```

* `open`을 했으면 `close` 도 꼭꼭
  * 사용 다 했으면 `close` 해줘~ 



#### (2) `with open`

```python
with open("test.txt", "wt", encoding="UTF-8") as f:
	text = f.read()
```

* `with` 구문을 나오게 되면 자동으로 `close` 해줌



---



## `write`

> 파일 쓰기

```python
f.write("원하는 문장")
```

* 파일 안에 데이터 입력



---



## `read`

> 파일 읽기

#### (1) `read()`

```python
f = open("live.txt", "rt", encoding="utf8")
text = f.read()
print(text)
f.close()
```

* 처음부터 끝까지 읽음

#### (2) `read(숫자)`

```python
f = open("test.txt", "rt", encoding="UTF-8")
while True:
    text = f.read(10)    # 10 문자씩 읽기
    if len(text) == 0: break    # 더이상 읽을 문자가 없으면 break
    print(text, end = '$')
f.close()
```

* 숫자 만큼의 문자씩 읽기
* `' '` 공백 포함

#### (3) `readline()`

```
f = open("test.txt", "rt", encoding="UTF-8")
text = ""
line = 1
while True:
    row = f.readline()    # 한 행씩 읽기
    if not row: break
    text += str(line) + " : " + row
    line += 1
f.close()
print(text)
```

* 한 행씩 읽기 
* 개행 기준

#### (4) `readlines()`

```python
f = open("live.txt", "rt", encoding="UTF-8")
rows = f.readlines()    # 모든 행을 읽어서 리스트로 리턴
for row in rows:
    print(row, end = '')
f.close()
```

* 모든 행을 읽어서 리스트로 리턴

* 개행 문자도 같이 읽어옴
  * 그래서 `print`시 `end=''` 없이 그냥 개행을 해주면 2번 개행된 모습을 볼 수 있다~

#### (5) 바로 객체 사용

```python
f = open("live.txt", "rt", encoding="UTF-8")
for line in f:    # _io.TextIOWrapper 객체도 리터러블함
    print(line, end = '')
f.close()
```

* `_io.TextIOWrapper 객체` 자체가 리터러블함
  * 그래서 `for문`을 사용한 `행단위`로 출력할 수 있음.
* 이 방법을 많이 사용함



---



## 이외 여러가지 사용

#### (1) `seek`

* 일의 원하는 위치로 이동
* 원하면 조사해서 채워넣기 ㅎㅎ

#### (2) `exists`

* 파일 존재 확인하기

```python
import os

if os.path.exists("test.txt") :
   print("파일이 존재합니다.")
else :
   print("파일이 존재하지 않습니다.")
```

#### (3) `copy`

* 파일 복사

```python
import shutil
shutil.copy("test_old.txt", "test_new.txt")
```



---



## 디렉토리

> 폴더

#### (1) `listdir`

* 해당 패스 안의 디렉토리 목록을 리스트로 반환

```python
import os

files = os.listdir("c:\\KHR\\PYTHONexam")
for f in files:
    print(f)
```



####  (2) `isdir`

* 디렉토리가 맞는지 확인
* 맞으면 True, 맞지 않으면 False를 반환

```python
import os

def dumpdir(path):
    files = os.listdir(path)
    for f in files:
        fullpath = path + "\\" + f
        if os.path.isdir(fullpath):
            print("[" + fullpath + "]")
            dumpdir(fullpath)
        else:
            print("\t" + fullpath)

dumpdir("c:\\KHR\\PYTHONexam")
```

```
디렉토리이면,
"[경로\디렉토리명]" 출력

디렉토리가 아니면,
"	경로\파일명" 출력
```



---



## 문자셋

> characterset
>
> 인코딩값

* 문자마다 부여한 코드값들을 모아 놓은 것으로 각 문자셋마다 고유 명칭이 있다.
* 기억하면 좋은 문자셋 명칭
  * `ansi(euc-kr, ksc5601, cp949)` : 영문 1바이트(ASCII값), 한글 2바이트
  * `utf-16` : 유니코드. 모든 나라의 언어에 대한 코드값을 통일화 시키자, 2바이트로 표현
  * `utf-8` : `utf-16`을 보완해서 나온 것. 1~4바이트로 표현

