# Map

* Key와 Value값으로 이루어진 구조

<br>

#### 정의

```java
Map<keyType, valueType> map = new HashMap<>();
```

<br>

#### 메소드

* `put()`
  * 원소 입력
  * `map.put(key, value);`
* `get()`
  * 키값 기반으로 value값 반환
  * 해당 키값을 가진 요소가 없으면 `null`값 반환
  * `map.get(key)`
* `containsKey()`
  * 특정 key가 존재하는지 확인
  * 해당 키값을 가진 요소가 있으면 `true`, 없으면 `false`값 반환 
  * `map.containsKey(key)`

<br>

#### Iterator

```java
Map<String, String> map = new HashMap<>();

Set<String> keys = map.keySet();
Iterator<String> it = keys.iterator();
while(it.hasNext()) {
	String key = it.next();
    if(key.equals(삭제하려는key)){
        it.remove(); // 삭제
    }
}
```

<br>

---

<br>

## 정렬

#### Key 기준 정렬

> `TreeMap` 을 이용하여 쉽게 Key 기준정렬

* 오름차순

  ```java
  TreeMap<Integer, Integer> map = new TreeMap<>();
  
  Iterator<Integer> itAsc = map.keySet().iterator(); 
  while (itDesc.hasNext())
  {
  	int key = itDesc.next();
  	// 코드
  }
  ```

* 내림차순

  ```java
  TreeMap<Integer, Integer> map = new TreeMap<>();
  
  Iterator<Integer> itDesc = map.descendingKeySet().iterator();
  while (itDesc.hasNext())
  {
  	int key = itDesc.next();
  	// 코드
  }
  ```

<br>

#### Value 기준 정렬

* 오름차순

  ```java
  Map<Integer, Integer> map = new HashMap<>();
  List<Integer> keySetDesc = new ArrayList<>(map.keySet());
  
  Collections.sort(keySetList, new Comparator<Integer>() {
  	@Override
  	public int compare(Integer o1, Integer o2) {
  		return map.get(o1).compareTo(map.get(o2));
  	}
  });
  
  for(Integer key : keySetList) {
  	// 코드
  }
  ```

* 내림차순

  ```java
  Map<Integer, Integer> map = new HashMap<>();
  List<Integer> keySetDesc = new ArrayList<>(map.keySet());
  
  Collections.sort(keySetList, new Comparator<Integer>() {
  	@Override
  	public int compare(Integer o1, Integer o2) {
  		return map.get(o2).compareTo(map.get(o1));
  	}
  });
  
  for(Integer key : keySetList) {
  	// 코드
  }
  ```

  



