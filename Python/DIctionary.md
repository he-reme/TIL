# 딕셔너리

> `dic = {키1:값1, 키2:값2, 키3:값3, ...}`
>
> 키(Key)와 값(Value) 형태로 데이터 저장



---



## 딕셔너리 사용 시 주의사항

* 키는 변경이 불가능한 자료형들(`int, float, tuple, str`)로만 만들어짐



---



## 딕셔너리 초기화

### (1) 형식

* `dic = {키1: 값1, 키2:값2, 키3:값3, ...}`
* 값에는 모든 데이터 타입 가능

### (2) 예시

```python
dictionary = {
    "name": "7D 건조 망고",
    "type": "당절임",
    "ingredient": ["망고", "설탕", "메타중아황산나트륨", "치자황색소"],
    "origin": "필리핀"
}
```



---



## 데이터 추가

* `dic[키] = 값`
  * 이미 추가된 `키`라면, 해당 값으로 **재할당**됨



---



## 키에 기반한 값 반환

### (1) `dic[키]`

* 딕셔너리에 없는 `키`일 경우 `error`



### (2) `dic.get()`

* 딕셔너리에 없는 `키`일 경우 `None`

* `dic.get(키)`
  * 딕셔너리에 없는 `키`일 경우 `None` 반환
* `dic.get(키, 기본값)`
  * 딕셔너리에 없는 `키`일 경우 설정한 `기본값`이 대신 반환됨

* 딕셔너리에 소속된 함수



## 여러 메소드

### (1) `items()`

* 딕셔너리의 모든 `키`와 `값`을 **튜플**로 묶어서 반환



### (2) `keys()`

* `키`만 반환



### (3) `values()`

* `값`만 반환



### (4) `del()`

* 해당 키를 가진 데이터 삭제
* `del(dic[키])`



---



## 다양한 출력 방법

### (1) 키 출력

```python
keylist = dic.keys()
for key in keylist:
    print(key)
```



### (2) 값 출력

```python
valuelist = dic.values()
for value in valuelist:
    print(value)
```



### (3) 키, 값 출력 1

```python
itemlist = dic.items()
for item in itemlist:
    print(item)
```



### (4) 키, 값 출력 2

```python
itemlist = dic.items()
for key,value in itemlist:
    print(key, value, sep="-")
```



---



## 리스트를 딕셔너리로 변환

### `dict()`

* `list = [[키1, 값1], [키2, 값2], [키3, 값3], ...]`
  * `dic = dict(list)`
* `list = [(키1, 값1), (키2, 값2), (키3, 값3), ...]`
  * `dic = dict(list)`
* `list = dict(키1=값1, 키2=값2, 키3=값3, ...)`
  * `dic = dict(list)`
  * 이 경우에는.. list 변수부터가 딕셔너리임



---



## 이차원 딕셔너리

> 정식 명칭(?)은 Json 형식 - 확인 필요

### (1) 형식

```python
dic = {
	키1: {
		키:값
		키:값
	}
	키2: {
		키:값
		키:값
	}
	...
}
```



### (2) 예시

```python
terrestrial_planet = {
    'Mercury': {
        'mean_radius': 2439.7,
        'mass': 3.3022E+23,
        'orbital_period': 87.969
    },
    'Venus': {
        'mean_radius': 6051.8,
        'mass': 4.8676E+24,
        'orbital_period': 224.70069,
    },
    'Earth': {
        'mean_radius': 6371.0,
        'mass': 5.97219E+24,
        'orbital_period': 365.25641,
    },
    'Mars': {
        'mean_radius': 3389.5,
        'mass': 6.4185E+23,
        'orbital_period': 686.9600,
    }
}
```



### (3) 값에 접근하기

* `dic[키1][키2]`

* 예시
  * `terrestrial_planet['Venus']['mean_radius']`

