# Comprehension

> 지능적으로 만들기



---



## 리스트 컴프리헨션 (List Comprehension)

### (1) `[값표현식 for 변수 in sequence범위]`

* 예시

  ```python
  list = [d*2 for d  in range(1,11)]
  ```



### (2)`[값표현식 for 변수 in sequence범위 if 조건식]`

* 예시

  ```python
  old_list = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
  list1 = [d for d in old_list if d%2]
  list2 = [d for d in old_list if d>5]
  list3 = [d for d in range(1,16) if not d%2]
  ```

  

### (3) `[값표현식1 if 조건식 else 값표현식2 for 변수 in sequence범위]`

* 예시

  ```python
  list = ['홀수' if d%2 else '짝수' for d in range(1,16)]
  ```

  

### (4) 중첩 반복문

* 예시

  ```python
  list = [i+j for i in range(0,10) for j in range(10,20)]
  ```

  

---



## 세트 컴프리헨션 (Set Comprehension)

### (1) `{값표현식 for 변수 in sequence범위}` 

* 예시

  ```python
  old_set = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
  list = {d for d in old_set if d%2}
  ```

  

### (2) `{값표현식 for 변수 in sequence범위 if 조건식}`

* 예시

  ```python
  set = {'홀수' if d%2 else '짝수' for d in range(1,16)}
  ```

  

### (3) `{값표현식1 if 조건식 else 값표현식2 for 변수 in sequence범위}`

* 예시

  ```python
  set = {'홀수' if d%2 else '짝수' for d in range(1,16)}
  ```

  

---



## 딕셔너리 컴프리헨션 (Dictionary Comprehension)

### (1) `{키표현식:값표현식 for 변수 in sequence범위}`

* 예시

  ```python
  students = dict(둘리=90, 또치=85, 도우너=95, 희동이=75, 마이콜=80)
  pass_students = {k:v for k,v in students.items()}
  # {'둘리':90, '또치':85, '도우너':95, '희동이':75, '마이콜':80}
  ```

  

### (2) `{키표현식:값표현식 for 변수 in sequence범위 if 조건식}`

* 예시

  ```python
  students = dict(둘리=90, 또치=85, 도우너=75, 희동이=75, 마이콜=80)
  pass_students = {k:v for k,v in students.items() if v>80}
  # {'둘리':90, '또치':85, '도우너':95}
  ```

  

### (3) `{키표현식:값표현식1 if 조건식 else 값표현식2 for 변수 in sequence범위}`

* 예시

  ```python
  scores = dict(둘리=90, 또치=85, 도우너=95, 희동이=75, 마이콜=80)
  grades = {name: 'PASS' if value > 80 else 'No-PASS' for name, value in scores.items()}
  # {'둘리':'PASS', '또치':'PASS', '도우너':'PASS', '희동이':'No-PASS', '마이콜':No-PASS}
  ```

  

### (4) 키와 값을 반대로 바꾸기

* 예시

  ```python
  students = dict(둘리=90, 또치=85, 도우너=75, 희동이=75, 마이콜=80)
  swap_students = { v : k for k, v in students.items() }
  # {90:'둘리', 85:'또치', 95:'도우너', 75:'희동이', 80:'마이콜'}
  ```

  