# Set

#### 특징

* 순서 없이 주머니에 구슬(데이터)를 넣는 형태

* 순서가 없으므로 데이터를 구별할 index가 없어 중복이 허용되지 않음

  * 효율적인 중복 데이터 제거 수단

* index가 없어서..

  * update 없음

  * 출력 시 넣은 순서대로 안나옴

<br>

#### 관련 클래스 관계도 (계층 구조)

* Set
  * HashSet
  * SrotedSet (이진트리로 정렬된 상태로 요소 관리 )
    * NavigableSet
    * TreeSet

<br>

#### 생성

```java
Set<Object> hset = new HashSet<Object>();
```

<br>

#### 동일한 데이터의 기준

1. 객체의 `equals()`가 `true`를 리턴하고,

2. `hashCode()` 값 또한 `true`를 리턴할 때

