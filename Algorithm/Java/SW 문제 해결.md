# SW 문제 해결

#### SW 문제 해결 역량?

* 프로그래밍을 하기 위한 많은 제약 조건과 요구사항을 이해하고 최선의 방법을 찾아내는 능력
* 프로그래머가 사용하는 언어나 라이브러리, 자료구조, 알고리즘에 대한 지식을 적재적소에 퍼즐을 배치하듯 이들을 연결하여 큰 그림을 만드는 능력
* 문제 해결 역량은 추상적인 기술!

<br>

---

<br>

## 알고리즘

#### 알고리즘을 표현하는 방법 두가지

* 의사코드
* 순서도

#### 좋은 알고리즘?

* 정확성 : 얼마나 정확하게 동작하는가
* 작업량 : 얼마나 적은 연산으로 원하는 결과를 얻어내는가 (시간복잡도)
* 메모리 사용량 : 얼마나 적은 메모리를 사용하는가 (공간복잡도)
* 단순성 : 얼마나 단순한가 (가독성)
* 최적성 : 더 이상 개선할 여지없이 최적화되었는가

<br>

---

<br>

## 알고리즘 성능

#### 복잡도의 점근적 표기

* 시간(또는 공간)복잡도는 입력 크기에 대한 함수로 표기하는데, 이 함수는 주로 여러 개의 항을 가지는 다향식
* 이를 단순한 함수로 표현하기 위해 점근적 표기를 사용함
* 입력 크기 n이 무한대로 커질 때의 복잡도를 간단히 표현하기 위해 사용하는 표기법

<br>

#### 빅오(O) 표기법

* 시간 복잡도 함수 중에서 가장 큰 영향력을 주는 n에 대한 항만을 표시
* 계수는 생략하여 표시
* 예
  * O(3n+2) = O(3n) = O(n)
  * O(2n^2 + 10n + 100) = O(n^2)
  * O(4) = O(1)
* 