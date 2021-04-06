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