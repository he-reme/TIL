# Map

#### 특징

* Key와 Value를 하나의 Entry로 묶어서 데이터 관리
  * Key : Object 형태로 데이터 중복을 허락하지 않음
  * Value : Object 형태로 데이터 중복이 허락됨.
* Map.Entry
  * Key + Value
* Key
  * Set으로 관리하면 좋음

<br>

#### 관련 클래스 관계도 (계층 구조)

* Map
  * Hashtable (요즘엔 잘 사용X)
    * Properites
  * HashMap
  * SortedMap
    * NavigableMap
      * TreeMap

<br>

#### 생성

```java
Map<String, String> hMap = new HashMap<>();
```



---

<br>

## 주요 메서드

#### 추가

* `put(K key, V value)`
  * 추가가 성공하면 null 반환
  * 추가가 실패하면(key 이미 존재) 이미 존재하는 key의 value 반환
* `putAll(Map<? extends K, ? extends V> m)`
* `pubIfAbsent(K key, V value)`
  * 기존에 없는 key일 경우 값 추가

<br>

#### 조회

* `containsKey(Object key)`

* `containsValue(Object value)`

* `entrySet()`

  * Key와 Value 값 반환

    ```java
    Set<Entry<String, String>> entries = hMap.entrySet();
    for(Entry<String, String> entry: entries) {
    	if(entry.getValue().equals("4567")) {
    		System.out.println("번호가 4567인 사람 : " + entry.getKey());
    	}
    }
    ```

* `keySet()`

  * 모든 key값 가져오기

    ```java
    Set<String> keys = hMap.keySet();
    for(String key: keys) {
    	System.out.println("key: " + key + ", value: " + hmap.get(key));
    }
    ```

* `get(Object key)`

  * key에 대한 value 가져오기
  * 없으면 null 반환

* `values()`

* `size()`

* `isEmpty()`

<br>

#### 삭제

* `clear()`
* `remove(Object key)`
  * key 값을 기반으로 요소 삭제

<br>

#### 수정

* `pub(K key, V value)`
* `putAll(Map<? extends K, ? extends V> m)`