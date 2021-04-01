# numpy

> 수치 데이터를 다루는 데 사용됨
>
> 수치 연산과 관련된 여러 메소드 제공

#### 임포트

```python
import numpy as np
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