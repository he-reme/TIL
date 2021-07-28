# Stream API

> 컬렉션을 람다식으로 표현하게 해줌

#### 스트림 API

* 자바 8에 추가된 java.util.stream 패키지
* I/O의 스트림과는 전혀 무관

<br>

#### 주요 목적

* 배열을 포함한 컬렉션(데이터 소스)의 저장 요소를 하나씩 참조해서 람다식으로 처리할 수 있도록 해줌

<br>

#### 스트림 API의 3단계

1. 생성

2. 중간 처리
   * 스트림을 변환(map)시키는 단계

3. 최종 처리
   * 스트림을 사용하는 단계

<br>

---

<br>

## 예시

```java
List<Book> list = new ArrayList<Book>();

...

list.stream().filter(i->i.getPrice()>20000).forEach(i -> {System.out.println(i);});
	
```

