# Spark

#### hadoop

* 분산 저장 분산 처리 시스템

* 클러스터
  * 여러 대의 컴퓨터들이 연결되어 하나의 시스템처럼 동작하는 컴퓨터들의 집합

* Hadoop MapReduce
  * 구글에서 대용량 데이터 처리를 분산 병렬 컴퓨팅에서 처리하기 위한 목적으로 제작한 소프트웨어 프레임워크
  * 페타바이트 이상의 대용량 데이터를 신뢰돡 낮은 컴퓨터로 구성된 클러스터 환경에서 병렬 처리를 지원하기 위해서 개발됨



---



## Apache Spark

* 메모리 내 처리를 지원하여 빅데이터를 분석하는 애플리케이션의 성능을 향상시키는 오픈 소스 병렬 처리 프레임워크

#### PySpark

* Apache Spark 기능을 사용하여 Python 애플리케이션을 실행하기 위해 Python으로 작성된 Spark 라이브러리
* PySpark를 사용하면 분산 클러스터에서 애플리케이션을 병렬로 실행할 수 있음
* `PySpark.md`에서 자세히..



---



## Spark의 데이터 처리 단위

> RDD

#### RDD

* Resilient Distributed Dataset, 내결함성 분산 데이터셋
* 데이터셋을 추상적으로 다루기위한 데이터셋
* RDD가 제공하는 API로 **변환**과 **액션** 기능을 구현
* Spark 에서 처리되는 데이터는 RDD 객체로 생성하여 처리함

#### RDD 객체 생성 방법- 2가지

1. Collection 객체를 만들어서
2. HDFS의 파일을 읽어서

#### RDD 객체의 특징

* **Read Only** (immutable, 불변)
* 1~n 개의 partition으로 구성 가능
* 병렬적(분산) 처리 가능
* RDD를 제어하는 연산 (2가지 타입)
  * **Transformation**
    * RDD에서 데이터를 조작하여 새로운 RDD를 생성하는 함수
  * **Action**
    * RDD에서 RDD가 아닌 타입의 data로 변환하는 함수
* Transformation은 **Lazy-execution**을 지원
  * 인터프리터에서 Transformation 명령어를 읽어 들일 때는 단순히 Lineage만 생성
  * Action 명령어가 읽히면, 쌓여있던 Lineage를 실행
* lineage를 통해 **fault tolerant(결함 내성)을 확보**
  * lineage만 기록해두면 동일한 RDD를 생성할 수 있음
  * RDD의 copy를 보관하기보다, Lineage만 보관해도 복구 가능
  * 일부 계산 비용이 큰 RDD는 디스크에 Check Pointing
  * reliablity 확보



---



## Transformation과 Action

#### Transformation

* 행위를 기록할뿐 연산작업이 실제 이루어지지 않음
* 기존 RDD를 이용해 새로운 RDD를 생성하는 연산
  * 연산의 수행 결과가 RDD
* **Lineage**를 만들어 가는 과정
* 변환, 필터링 등의 작업들
  * 맵, 그룹화, 필터, 정렬, ...

```
map(func)
flatMap(func)
filter(func)
groupByKey()
reduceByKey(func)
mapValues(func)
sample(...)
union(other)
distinct()
sortByKey()
```

#### Action

* api가 호출되면 이때 모든 작업을 최적화된 경로로 수행

* 연산의 수행 결과가 정수, 리스트, 맵 등 RDD가 아닌 다른 타입이면 Action
* **Lineage를 실행하고 결과를 만듬**
* first(), count(), collect(), reduce(), ...

```
reduce(func)
collect()
count()
first()
take(n)
saveAsTextFile(path)
countByKey()
foreach(func)
```



---



## Lazy-execution

> Action 연산이 실행되기 전에는 Transformation 연산이 처리되지 않는 것을 의미

* Transformation 연산은 관련 메서드를 호출하여 연산을 요청해도, 실제 수행은 되지 않고 연산 정보만 보관
  * 이렇게 Transformation 연산 정보를 보관한 것을 Lineage라고 함

* 보관만 하다가 첫 번째 Action 연산이 수행될 때 모든 Lineage에 보관된 Transformation 연산을 한 번에 처리함
* Lazy-execution과 Lineage를 활용함으로써
  * 처리 효율을 높이고
  * 클러스터 중 일부 고장으로 작업이 실패해도 Lineage를 통해 데이터를 복구함

#### Lineage

* Transformation 연산 정보를 보관한 것
* operation의 순서를 기록해 DAG로 표현한 것



---



## 주요 함수

* `parallelize()`
  * 스칼라 컬렉션 객체를 이용해서 **RDD 객체 생성**
* `count()`
  * RDD의 요소 개수를 리턴
* `first()`
  * RDD 객체의 첫 번째 요소를 리턴
* `collect()`
  * RDD 객체의 모든 요소를 리스트로 리턴
* `map()`
  * 입력 RDD의 모든 요소에 f를 적용한 결과를 저장한 RDD를 반환
* `flatMap()`
  * 입력 RDD의 모든 요소에 f를 적용하고 모든 요소들을 하나로 묶어서 반환
* `filter()`
  * 입력 RDD의 모든 요소에 f를 수행하고 참을 리턴하는 결과만 저장한 RDD를 반환
* `reduce()`
  * 저장된 f를 수행시켜 입력 RDD의 개수를 축소시켜서 생성된 RDD를 반환


