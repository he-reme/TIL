# 배열

#### Array is immutable

* **최초 메모리 할당 이후, 변경할 수 없음**
* 개별 요소는 다른 값으로 변경이 가능하나, 삭제할 수는 없음
* 크기를 늘리거나 줄일 수 없음
  * 연속적인 주소를 새로 받을 수 없기 때문에

<br>

---

<br>

## 배열 생성과 초기화1

#### 생성

* `new` 키워드와 함께 배열의 데이터 타입 및 크기 지정
  * `data_type[] arr = new data_type[length]`
* `[]`의 위치는 상관 없으나 가급적 타입 바로 뒤에 붙이도록!

<br>

#### 초기화

* 배열을 생성과 동시에 자료형에 대한 default 초기화 진행
  * boolean : `false`
  * char : 공백문자
  * byte, short, int : `0`
  * long : `0L`
  * float : `0.0f`
  * double : `0.0`
  * 참조형 변수 : `null`

<br>

---

<br>

## 배열 생성과 초기화2

> 예시와 주의점

#### 생성과 동시에 할당한 값으로 초기화

```java
int[] arr = {1, 3, 5, 6, 8}
int[] arr = new int[]{1, 3, 5, 6, 8}
```

<br>

#### 선언 후 생성 시 초기화 주의

* **중괄호 초기화**는 **배열 생성할 때 같이** 해줘야 사용 가능

* 선언과 동시 초기화

  ```java
  int[] arr = {1, 3, 5, 6, 8}
  int[] arr = new int[]{1, 3, 5, 6, 8}
  ```

* 컴파일 오류 예시

  ```java
  int[] arr;
  arr = {1, 3, 5, 6, 8}
  ```

  ```java
  int[] arr; // 배열의 크기를 알수 없는데
  arr = new int[]{1, 3, 5, 6, 8} // 초기화시킴
  ```

  * 선언할 때 배열의 크기를 알 수 없을 때도 불가능

<br>

---

<br>

## 배열의 사용

#### 각 요소에 접근

* `index` 번호를 가지고 접근
* `0`부터 시작

<br>

#### 배열의 크기

* `arr.length`

<br>

#### 배열 한번에 출력

* `Arrays.toString(arr)`

<br>

#### for-each를 이용한 출력 및 접근

* 가독성이 개선된 반복문

* 배열 및 Collections에서 사용

  * index 대신 직접 요소에 접근하는 변수를 제공

* naturally ready only (copied value)

* 사용

  ```java
  int arr[] = {1, 3, 6, 7, 9};
  for(int x : arr) {
  	System.out.println(x);
  }
  ```

<br>

---

<br>

## 배열 복사 및 새로운 메모리 생성

> 배열의 크기를 늘리는 방법 (실제로 늘리는 것이 아님)
>
> * 배열 복사를 사용하거나
> * 새로운 메모리를 생성함으로써
>
> 크기를 늘린 것 처럼 보이는 방법

#### 1. 배열 복사

* `System.arraycopy`

  * api 제공하는 배열 복사 method

    ```java
    public static void arraycopy( Object src, int srcPos, Object dest, int destPos, int length);
    ```

  * 예시

    ```java
    int[] arr_copy = new int[4];
    System.arraycopy(d, 0, arr_copy, 0, arr.length);
    ```

  * 크기 2배 늘리고 카피하는 방법

    ```java
    int[] arr_copy = new int[d.length * 2];
    System.arraycopy(d, 0, arr_copy, 0, arr.length);
    ```

* `Arrays.copyOf`

  * 정의

    ````java
    arr = Arrays.copyOf(복사할 배열, 원하는 길이)
    ````

  * 예시

    ```java
    d = Arrays.copyOf(d, 5); 
    ```

* `clone`

  ```java
  int [] d_copy = d.clone();
  ```

<br>

####  2. 새로 할당

* 다른 배열 메모리 생성되고 거기를 가리키게 됨

* 기존에 가리키던 것은 가비지 컬렉터에 의해 수거됨

* 새로 할당

  ```java
  int[] d = {1, 3, 5, 6, 8}
  d = new int[]{10, 12, 14};
  ```

<br>

---

<br>

## 2차원 배열

#### 생성

* 가능한 것

  ```java
  int arr[][] = new int[4][3];
  int [] arr[] = new int[4][3];
  int [][] arr = new int[4][3];
  int [][] arr = new int[][] {{1, 2, 3}, {1, 2, 3}, {1, 2, 3}, {1, 2, 3}};
  int [][] arr = {{1, 2, 3}, {1, 2, 3}, {1, 2, 3}, {1, 2, 3}};
  ```

* 불가능한 것

  ```java
  int [][] arr = new int[4]{1,2,3};
  ```

#### 4X? 배열 생성

1. 1차 생성

   ```java
   int [][] arr = new int[4][]
   ```

2. 2차 생성

   ```java
   arr[1] = new int[2];
   arr[2] = new int[4];
   arr[3] = new int[3];
   ```

   * 초기화는 안됨

     ```java
     arr[3] = {1, 2, 3}; // (X)
     ```

<br>

---

<br>

## 정렬

* 오름차순

  `Arrays.sort(arr)`

* 사용자 지정 정렬

  ```java
  Integer[] arr = {8, 9, 4, 2, 11, 7, 1, 3};
  Arrays.sort(arr, new Comparator<Integer>(){
  	@Override
  	public int compare(Integer a, Integer b){
  		return b-a;
  	}
  });
  ```

  * 람다식으로 표현

    ```java
    Arrays.sort(arr, (a, b) -> return b-a;});
    ```

  * `return a-b` : 오름차순
  * `return b-a`  : 내림차순

* 객체 정렬

  ```java
  class Book implements Comparable<Book>{
  	String title;
  	int price;
  	
      public Book(){}
      
  	// price 기준으로 정렬
  	@Override
  	public int compareTo(Book a) {
  		return price - a.price;
  	}
  }
  ```

  

<br>

---

<br>

## String을 배열로

* String을 배열로

  `toArray(str)`

* String을 char 배열로

  `toCharArray(str)`

<br>

---

<br>

## 응용

* Array 순회/탐색
  * 주변 탐색 (상하좌우 등등)

