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

