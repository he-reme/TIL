# numpy

> 수치 데이터를 다루는 데 사용됨
>
> 수치 연산과 관련된 여러 메소드 제공

* 행렬이나 대규모 다차원 배열을 쉽게 처리 할 수 있도록 지원하는 파이썬 라이브러리
* 데이터 구조 외에도 수치 계산을 위해 효율적으로 구현된 기능을 제공
* 다차원 행렬 자려구조인 ndarray 객체를 핵심으로 선형대수 연산이 필요한 함수들을 제공

#### Python List

* 여러가지 타입의 원소
* linked List 구현
* 메모리 용량이 크고 속도가 느림
* 벡터화 연산 불가

#### Numpy ndarray

* 동일 타입의 원소
* contiguous memory layout
* 메모리 최적화, 계산 속도 향상
* 벡터화 연산 가능

#### 임포트

```python
import numpy as np
```



---



## 벡터

#### 행으로 구성된 벡터 

* 1차원 ndarray 객체

  ```
  vector_row = np.array([1, 2, 3])
  ```

#### 열로 구성된 벡터

* 2차원 ndarray 객체

  ```
  vector_column = np.array([[1],
  						  [2],
  						  [3]])
  ```

#### 메소드

```
print(ndarray객체.ndim)
print(ndarray객체.size)
```





---



## 메소드

* `np.arange(시작, 끝, step)`
  * 끝은 포함하지 않음
  * like, 파이썬의 `range()`

* `np.random.normal(loc, scale, size)`
  * 난수 생성
  * `loc`
    * 평균
  * `scale`
    * 표준편차
  * `size`
    * 뽑을 갯수

* `np.empty((행, 열))`
  * 비어있는 ndarry 객체 생성
* `np.zero((행, 열))`
  * 0으로 초기화된 ndarray 객체 생성
* `np.ones((행, 열))`
  * 1로 초기화된 ndarray 객체 생성

* `new_ndarray = np.array(ndarray)`
  * 복제
* `same_ndarray = np.asarray(ndarray)`
  * 참조

* 난수 생성

  * 초기값 지정 (난수 생성 이전 꼭 쓰기)

    ```
    np.random.seed(0)
    ```

  * 0.0과 1.0 사이에서 n개의 실수 난수 뽑기

    ```
    np.random.random(n)
    ```

  * 0.0과 1.0 사이에서 5행 2열 구조의 실수 난수 뽑기

    ```python
    np.random.rand(5,2)
    ```

  * 0과 10 사이에서 n개의 정수 난수 뽑기

    ```python
    np.random.randint(0, 11, n)
    ```

  * 0과 10 사이에서 5행 2열 구조의 정수 난수 뽑기

    ```python
    np.random.randint(0, 11, (5,2))
    ```

  * 평균이 0.0이고 표준 편차가 1.0인 정규 분포에서 세 개의 수

    ```python
    np.random.normal(0.0, 1.0, 3)
    ```

  * 해당 리스트에서 5개의 난수 뽑기 (중복 가능)

    ```python
    np.random.choice([0,1,2], 5)
    ```

  * 미분 적분??

    ```python
    a = np.array([0, 1, 2, 3, 4])
    np.random.shuffle(a)
    print(a)
    ```

    

---



## 인덱싱

```python
vector = np.array([1,2,3,4,5,6,7,8,9])
```

* `vector[0]`
* `vector[:]` : 모든행 추출
* `vector[3:]`
* `vector[:3]`
* `vector[-1]`
* `vector[-4:-1]`

```
matrix = np.array([1,2,3]
				  [4,5,6]
				  [7,8,9])
```

* `matrix[0,0]`
* `matrix[:2, :]`
* `matrix[:, 1:2]`
* `matrix[2]`
* `matrix[[0,2]]` : 1, 3번째 항 선택
* `matrix[[0,2], [1,0]]`



---



## 조건식 행 선택

```python
mask = matrix > 5
matrix[mask]
```

```python
matrix[matrix > 5]
```



---



## `reshape()`

> 데이터 변경 없이 지정된 shape으로 변환하는 메서드

```python
matrix = np.array([[1, 2, 3],
                   [4, 5, 6],
                   [7, 8, 9]])
m1 = matrix[matrix>5] # [6, 7, 8, 9]
m2 = m1.reshape(2,2) # [[6, 7][8, 9]]
```

* m1을 (2행,2열) 형태로 만들어 m2에 복제



---



## 통계 함수

* `np.max(matrix)`

  * `np.max(matrix, axis=0)`
    * 열단위로 최대값 추출
  * `np.max(matrix, axis=1)`
    * 행단위로 최대값 추출
  * `keepdims=True` 옵션
    * 차원 유지 (열 유지)

* `np.min(matrix)`

* `np.mean(matrix)` : 평균

  * `axis` 사용 가능

* `np.var(matrix)` : 분산

* `np.std(matrix)` : 표준 편차

* `np.vectorize()`

  * 함수 호출을 통해 배열의 값을 재구성함

  ```python
  matrix = np.array([[1, 2, 3],
                     [4, 5, 6],
                     [7, 8, 9]])
  ```

  ```python
  add100 = lamda i ; i+100 if i%2==1 else i # 함수
  vectorized_add100 = np.vectorize(add100) # 함수 호출을 통해 배열의 값을 재구성 함. 함수 등록 ?
  print(vectorized_add100(matrix))
  ```



---



## 연산

* 전치

  ```python
  matrix.T
  matrix.transpose()
  ```

* 덧셈

  ```python
  m1 + m2
  np.add(m1, m2)
  ```

* 뺄셈

  ```python
  m1 - m2
  np.subtract(m1, m2)
  ```

* 곱셈

  ```
  m1 * m2
  ```

* 행렬곱

  ```python
  m1 @ m2
  np.dot(m1, m2)
  ```

  

---



## 여러 정보 출력

* 행렬의 원소 개수

  ```python
  matrix.size
  ```

* 행렬의 크기

  ```python
  matrix.shape
  ```

  * 출력 : `(행, 열)`

* 차원의 수

  ```python
  matrix.ndim
  ```

* 행렬 안의 원소의 타입

  ```python
  matrix.dtype
  ```

  

---



## 이미지 로드

```python
from PIL import Image    
r2d2 = np.array(Image.open('data/r2d2.JPG')) 
print(r2d2)
```



