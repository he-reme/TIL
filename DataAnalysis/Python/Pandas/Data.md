# 데이터 입출력

* 판다스는 다양한 형태의 외부 파일을 읽어와서 **데이터프레임을 변환**하는 함수를 제공
* 어떤 파일이든 데이터프레임으로 변환되고 나면, 판다스의 모든 함수와 기능을 자유롭게 사용할 수 있음
* 반대로, 데이터프레임을 다양한 유형의 파일로 저장할 수도 있음



---



## 판다스 데이터 입출력 도구

> Reader : 함수
>
> Writer : 메소드

#### CSV

* Reader : `read_csv`
* Writer : `to_csv`

#### JSON

 * Reader : `read_json`
 * Writer : `to_json`

#### HTML

* Reader : `read_html`
* Writer : `to_html`

#### Local clipboard

* Reader : `read_clipboard`
* Writer : `to_clipboard`

#### MS Excel

* Reader : `read_excel`
* Writer : `to_excel`

#### HDF5 Format (하둡에 저장되어있는 파일)

* Reader : `read_hdf`
* Writer : `to_hdf`

#### SQL

* Reader : `read_sql`
* Writer : `to_sql`



---



## CSV 파일

>  데이터 값을 쉼표`,` 로 구분하고 있는 텍스트 파일
>
> `,`로 열을 구분하고 `줄바꿈`으로 행을 구분

#### 읽기

```python
pd.read_csv("파일경로.csv")
```

* 옵션
  * `path`
  * `sep`
    * 텍스트 데이터를 필드별로 구분하는 문자
    * CSV 파일에 따라서 `,` 대신, 탭`\t` 이나 공백`" "`으로 텍스트를 구분하기도 함
  * `header`
    * 열 이름으로 사용될 행의 번호
    * `0` : 0행을 열로 지정
    * `1` : 1행을 열로 지정
    * `None` : 행을 열로 지정하지 않음
      * 0부터 열 이름 자동 지정
  * `index_col`
    * 행 인덱스로 사용할 열의 번호 또는 열이름
    * `False` : 0부터 숫자 인덱스 자동 지정
      * `열이름` : CSV파일이 가지고 있는 해당열을 인덱스로 지정
  * `encoding`
    * 텍스트 인코딩 종류를 지정

#### 저장 

```python
df.to_csv("파일경로.csv")
```

* 옵션
  * `index=None`
    * 인덱스 없이 저장
  * `header=None`
    * 컬럼 없이 저장

---



## Excel 파일

#### 읽기

```python
pd.read_excel("파일경로.xlsx")
```

* header 옵션을 추가하지 않은 경우
  * 첫 행이 열 이름을 구성함

#### 저장

```python
df.to_excel("파일경로.xlsx")
```

#### 여러 개의 데이터프레임을 하나의 Excel 파일로 저장

```python
writer = pd.ExcelWriter("파일경로.xlsx")
df1.to_excel(writer, sheet_name='sheet1')
df2.to_excel(writer, sheet_name='sheet2')
```

* 하나의 Excel 파일에 여러 시트로 저장

* `ExcelWriter()` 함수

  * Excel 워크북 객체 (Excel 파일) 생성

* `to_excel`

  * 인자

    * Excel 워크북 객체
    * `sheet_name` 옵션

    

---



## JSON

>  JavaScript에서 유래한 데이터 공유를 목적으로 개발된 특수한 파일 형식
>
> 파이썬 딕셔너리와 비슷하게 `Key:Value` 구조를 가짐

#### 읽기

```python
pd.read_json("파일경로.json")
```

#### 저장

```python
df.to_json("파일경로.json")
```

* 열 이름이 `Key` 가 됨
* 행이름(Key)과 데이터(Value)는 딕셔너리 형태로 `Value`가 됨



---



## HTML

#### 읽기

```python
pd.read_html("URL 또는 파일경로.html")
```

* **HTML 웹 페이지에 있는 `<table>` 태그에서 표 형식의 데이터**를 모두 찾아서 데이터 프레임으로 변환

* 한 페이지 내에 **여러 표**가 있는 경우
  * 각각 별도의 데이터 프레임으로 변환 되기 떄문에
  * **여러 개의 데이터프레임을 원소로 갖는 리스트가 반환됨**

#### 저장

```
df.to_html("")
```



---



## API 활용하여 데이터 수집하기

