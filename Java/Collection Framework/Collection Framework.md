# Collection Framework

#### 자료구조

* 배열
  * 가장 기본적인 자료구조
  * homeogeneous collection
    * 동일한 데이터 타입만 관리 가능
    * 타입이 다른 객체를 관리하기 위해서는 매번 다른 배열 필요
  * Polymorphism
    * Object를 이용하면 모든 객체 참조 가능
      * Collection Framework
    * 담을 때는 편리하지만 빼낼 때는 Object로만 가져올 수 있음
    * 런타임에 실제 객체의 타입 확인 후 사용해야 하는 번거로움
  * Generic을 이용한 타입 한정
    * 컴파일 타임에 저장하려는 타입 제한
    * 형 변환의 번거로움 제거

<br>

---

<br>

## Collection Framework

* java.util 패키지
  * 다수의 데이터를 쉽게 처리하는 방법 제공
  * DB 처럼 CRUD 기능 중요
  * 계층 구조 : `Iterable` - `Collection` - `[List, Set, Map]`

<br>

---

<br>

## collection framework 핵심 interface

#### 3대 주요 인터페이스

* List
* Set
* Map

#### List

* 순서가 있는 데이터의 집합. 
* 순서가 있으므로 데이터의 중복을 허락
* `ArrayList`, `LinkedList`

#### Set

* 순서를 유지하지 않는 데이터의 집합. 
* 순서가 없어서 같은 데이터를 구분할 수 없으므로 중복을 허락하지 않음
* `HashSet`, `TreeSet`

#### Map

* key와 value의 쌍으로 데이터를 관리하는 집합
* 순서는 없고 key의 중복 불가, value는 중복 가능
* `HashMap`, `TreeMap`

<br>

---

<br>

## Collection interface

#### 추가

* `add(E e)`
* `addAll(Collection<? extends E> c)`

#### 조회

* `contains(Object o)`
* `containsAll(Collection<?> c)`
* `equals()`
* `isEmpty()`
* `iterator()`
* `size()`

#### 삭제

* `clear()`
* `removeAll(Collection<?> c)`
* `retainAll(Collection<?> c)`

#### 수정

#### 기타

* `toArray()`