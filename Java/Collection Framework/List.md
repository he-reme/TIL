# List

#### 특징

* 순서가 있는 데이터의 집합
* 순서가 있으므로 데이터의 중복을 허락

<br>

#### 관련 클래스 관계도 (계층 구조)

* Collection 
  * List
    * Vector (요즘엔 잘 사용 X)
      * Stack
    * ArrayList
    * LinkedList
  * Queue
    * Deque
      * LinkedList

<br>

#### 생성

```java
List<String> aList = new ArrayList<>();
List<String> lList = new LinkedList<>();
```

<br>

---

<br>

## 주요 메서드 (`list.XXX()`)

#### 추가

+ `add([int index], E element)`
  + index를 써주면 끼워넣기
+ `addAll(int index, Collection<? extends E> c)`

#### 조회

+ `get(int index)`
  * 다른 접근 방법 : `for(E element: list)`
+ `indexOf(Object o)`
+ `contains(Object o)`  
  + 해당 요소를 포함하고 있으면 true 반환
+ `lastIndexOf(Object o)`
+ `listIterator()`

#### 삭제

+ `remove(int index)`

#### 수정

+ `set(int index, E element)`

#### 기타

+ `subList(int fromIndex, int toIndex)`

<br>

---

<br>

## ArrayList & LinkedList

#### ArrayList

* constructor
  * 내부적으로 Object[]에 저장
* add → ensureCapacityInternal → ensureExplicitCapacity → grow
  * 칸이 부족하면 알아서 늘려줌

<br>

#### LinkedList

* 각 요소를 Node로 정의하고 Node는 다음 요소의 참조 값과 데이터로 구성됨
  * 각 요소가 다음 요소의 링크 정보를 가지며 연속적으로 구성될 필요 없다
* 데이터 삭제 및 추가 : 참조값을 바꿈

<br>

#### ArrayList 와 LinkedList

* **ArrayList**
  * 순차 추가/수정/삭제 : 빠름
  * 비 순차 추가/수정/삭제 : 느림
  * 조회 : 빠름
* **LinkedList**
  * 순차 추가/수정/삭제 : 느림
  * 비 순차 추가/수정/삭제 : 빠름
  * 조회 : 느림

* **결론**
  * 특정 클래스가 좋고 나쁨이 아닌, 용도에 적합하게 사용해야 함
  * 소량의 데이터를 가지고 사용할 경우 큰 차이 X
  * ArrayList : 정적인 데이터 활용, 단순한 데이터 조회용
  * LinkedList : 동적인 데이터 추가, 삭제가 많은 작업

<br>

---

<br>

## 배열과 ArrayList

#### 배열의 장점

* 가장 기본적인 형태의 자료 구조로 간단하며 사용이 쉬움
* 접근 속도가 빠름

<br>

#### 배열의 단점

* 크기를 변경할 수 없어, 추가 데이터를 위해 새로운 배열을 만들고 복사해야 함
* 비 순차적 데이터의 추가, 삭제에 많은 시간이 걸림

<br>

#### ArrayList

* 배열을 사용하는 **ArrayList**도 태생적으로 배열의 장단점을 그대로 가져감

<br>

---

<br>

## 자료 삭제 시 주의사항

#### index를 이용한 for문

* 삭제를 하면 index가 앞으로 당겨지기 때문에
* index를 이용한 for문 삭제는 유의해야 함!
* **뒤에서부터 거꾸로 접근하면 괜찮다!**

#### forEach 문장

* read only !!!

<br>