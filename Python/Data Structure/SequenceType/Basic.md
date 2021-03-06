# 시퀀스 형

> 여러 자료를 순서대로 넣는다는 뜻



## 종류

* **문자열** - 불변
* **리스트**  - 가변
* **튜플** - 불변



## 기본

### (1) `요소 in 시퀀스형`

* 시퀀스형 안에 요소가 있는 경우, `True`

* 시퀀스형 안에 요소가 없는 경우, `False`

  

### (2) `요소 not in 시퀀스형`

* 시퀀스형 안에 요소가 없는 경우, `True`
* 시퀀스형 안에 요소가 있는 경우, `False`



### (3) `+` 

* `시퀀스형 + 시퀀스형`

* 같은 종류의 시퀀스형이어야 함
* 두 개의 시퀀스를 연결



### (4)  `*`

* `시퀀스형 * 숫자`
* 시퀀스형을 숫자만큼 반복 해 연장



### (5) 인덱싱

* `str[0]`, `str[1]`, `str[2]` , ...
* `list[0]`, `list[1]`, `list[2]`, ...
* `tuple[0]`, `tuple[1]`, `tuple[2]`, ...



### (6) 슬라이싱

* `str[i:j]`, `str[i:j:z]`, `str[:j:z]` , `str[i:]`, `str[::z]`, ...
* `list[i:j]`, `list[i:j:z]`, `list[:j:z]` , `list[i:]`, `str[::z]`, ...
* `tuple[i:j]`, `tuple[i:j:z]`, `tuple[:j:z]` , `tuple[i:]`, `tuple[::z]`, ...



### (7) `len(시퀀스형)`

* 길이 반환



### (8) `min(시퀀스형)`

* 최소값 반환



### (9) `max(시퀀스형)`

* 최대값 반환



### (10) `시퀀스형.count(요소)`

* 지정한 요소의 갯수 반환