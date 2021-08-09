# OPP (1)

#### 객체

* 주체가 아닌 것, 주체가 활용하는 것

#### 객체지향 프로그래밍

* 주변의 많은 것들을 객체화해서 프로그래밍하는 것
* 장점
  * 블록 형태의 모듈화된 프로그래밍
  * 신뢰성 높은 프로그래밍이 가능
  * 추가/삭제/수정이 용이
  * 재사용성이 높음

#### 현실 세계 객체, 클래스, 프로그램의 객체(instance, object)의 관계

* 현실의 객체가 갖는 속성과 기능은 추상화되어 클래스에 정의됨
* 클래스는 구체화되어 프로그램의 객체(instance, object)가 됨
* 현실의 객체는 우리가 만지고 느낄 수 있는 것
  * 실생활에 구체화 되어있는 내용

* 프로그램의 클래스와 객체
  * **클래스**
    * 객체를 정의해 놓은 것. 즉, 설계도/틀
    * 클래스는 직접 사용할 수 없고 직접 사용되는 객체를 만들기 위한 틀을 제공할 뿐
  * **객체**
    * 클래스를 데이터 타입으로 메모리에 생성된 것
    * 클래스를 구체화/객체화 시킨게 객체!

#### 객체 구조

* 상태, 속성 : **변수**, 필드
* 기능, 행위 : **메서드**, 함수

<br>

---

<br>

## 객체 생성과 메모리

#### JVM의 메모리 구조

> 이곳 저곳에 설명 적어놨으니 찾아보기

* **class area**
  * 클래스의 원형 로딩
  * Field 정보
  * Method 정보
  * 타입 정보
  * 상수 풀

* **stack**
  * 메서드들의 실행 공간
  * thread 별로 별도 관리
  * 메서드 호출 순서대로 쌓이는 구조
  * 메서드 프레임에 ㄹ로컬 변수도 쌓이는 구조
  * 로컬 변수는 선언된 영역을 벗어나면 삭제

* **heap**
  * 객체를 저장하기 위한 영역
  * thread에 의해 공유
  * 생성된 객체는 프로그래머가 삭제할 수  없고 **GC** 만이 제어 가능

<br>

---

<br>

## 변수의 종류

#### 선언 위치에 따른 분류

```java
public class VariableTypes {
	static int classVariable; // 클래스 멤버 변수
	int instanceVariable; // 인스턴스 멤버 변수
	
	public static void main(String[] args) { // 파라미터 변수
		int localVariable = 10; // 로컬 변수
		for(int i=0; i<100; i++) { // 로컬 변수
			System.out.println(i);
		}
	}
}
```

* **멤버 변수**
  * 클래스 멤버 변수
    * 클래스 영역
    * `static` 키워드 사용
  * 인스턴스 멤버 변수
    * 클래스 영역
* **지역 변수**
  * 지역 변수
    * 함수 내부
  * 파라미터 변수
    * 함수 선언부

<br>

#### 1. 인스턴스 멤버 변수 특징

* 선언 위치
  * 클래스 `{}` 영역에 선언

* 변수의 생성
  * 객체가 만들어질 때 객체 별로 생성됨
  * 생성 메모리 영역 : heap
* 소멸 시점
  * Garbage Collector에 의해 객체가 없어질 때
  * 프로그래머가 명시적으로 소멸시킬 수 없음

<br>

#### 2. 클래스 멤버 변수 특징

* 선언 위치
  * 클래스 `{}` 영역에 선언
  * `static` 키워드 붙임
* 변수의 생성
  * 클래스 영역에 클래스 로딩 시 메모리 등록
  * 개별 객체의 생성과 무관
  * 모든 객체가 공유하게 됨 (공유 변수라고도 불림)
* 변수에 접근
  * `클래스명.변수명`
* 소멸 시점
  * 프로그램 종료 시

<br>

#### 3. 지역 변수 & 파라미터 변수

* 선언 위치
  * 클래스 영역의 `{}` 이외의 모든 중괄호 안에 선언되는 변수들
* 변수의 생성
  * 선언된 라인이 실행될 때
  * 생성 메모리 영역 : thread 별로 생성된 stack 영역
* 소멸 시점
  * 선언된 영역인 `{}` 을 벗어날 때

<br>

---

<br>

## 메서드

> 현실의 객체가 하는 동작을 프로그래밍 화한 것
>
> 어떤 작업을 수행하는 명령문의 집합

#### Variable arguments

* 가변 인자

* 배열처럼 처리

* 가변인자를 사용하는 경우 오버로딩을 안하는 것이 좋다

* 메서드 선언 시 몇 개의 인자가 들어올 지 예상할 수 없을 경우 (가변적)

  * 배열 타입을 선언할 수 있으나, 메서드 호출 전 배열을 생성/초기화 해야하는 번거로움

* **`...`을 이용해 파라미터를 선언**

  * 호출 시 넘겨준 값의 개수에 따라 자동으로 배열 생성 및 초기화

  ```java
  public void vairableArgs(int... params) {
  	int sum = 0;
  	for(int i : params) {
  		sum += i;
  	}
  	System.out.println(sum);
  }
  ```

* 매개변수들 중 마지막 위치에서만 사용 가능

  ```java
  public int vairableArgs(int x, char c, int ... a) {
  	int sum = 0;
  	for(int data : a) {
  		sum += data;
  	}
  	return sum;
  }
  ```

  

<br>

#### 메서드 접근

* `static` / `non static` 상태를 구분해서 호출

  * `static` 메서드

    * 소속 : 클래스
    * 접근 방법
      * 클래스 내부의 static 메서드인 경우 : `메소드명`으로 바로 호출
      * 다른 클래스에서 호출할 경우 : `클래스명.메소드명`

  * `non static` 메서드

    * 소속 : 객체

    * 접근 방법
      * 클래스 내부의 메서드인 경우 : `메소드명`으로 바로 호출
      * 다른 클래스에서 호출할 경우 : `객체명.메소드명`

* 호출 시 가장 중요한 것은 **메모리에 있는가**

  * `static` 메서드
    * 언제나 메모리에 있음
    * 클래스 로딩 시 자동 등록
  * `non static` 메서드
    * 객체 생성 전에는 메모리에 없음
    * 객체 생성 시 모든 일반 멤버들은 메모리에 생성됨
    * 객체(레퍼런스)를 통해 접근

<br>

#### 메서드 호출 스택

* 스택
  * First in Last out 구조
* 메서드 호출 스택
  * 각각의 메서드 호출 시 마다 메서드 동작을 위한 메모리 상자를 하나씩 할당
  * 예시
    * 만약 `A메서드`에서 새로운 `B메서드` 호출 시
    * `A메서드`의 메모리 상자위에 `B메서드` 실행을 위한 메모리 상자를 쌓음
    * `A메서드`의 메모리 상자 비활성화(일시 정지)되고,
    * 맨 위에 있는 `B메서드` 메모리 상자 활성화
    * `B메서드`가 리턴하게 되면 `B메서드` 메모리 상자가 제거되면서 메모리 반납됨
    * 다시 `A메서드`가 맨 위가 되므로 활성화됨

<br>

#### 기본형 변수와 참조형 변수

* 메서드 호출 시 파라미터로 입력된 값을 복사해서 전달
* 자바는 call by value임!!!

<br>

---

<br>

## 메서드 오버로딩

#### **overloading**

* 동일한 기능을 수행하는 메서드의 추가 작성
* 동일한 기능을 여러 형태로 정의해야 한다면???

<br>

#### 장점

* 기억해야 할 메서드가 감소하고, 중복 코드에 대한 효율적 관리 가능

<br>

#### 방법

* **메서드 이름**
  * 동일
* **파라미터의 개수/순서/타입**
  * 달라야 할 것
* **리턴타입**
  * 의미 없음

<br>

---

<br>

## 생성자

#### 생성자

* 객체를 생성할 때 호출하는 메서드

  * new 키워드와 함께 호출되는 것

    `Person person = new Person();`

  * 일반 멤버 변수의 초기화나 객체 생성 시 실행돼야 하는 작업 정리

* 작성 규칙

  * 메서드와 비슷하나
  * 리턴 타입이 없고, 이름은 클래스 이름과 동일

<br>

#### 생성자 종류

* **기본 생성자**
  * 직접 생성 하지 않으면, 컴파일러가 구현부가 비어있는 기본 생성자 제공

* **파라미터가 있는 생성자**
  * 생성자 호출 시 값을 넘겨줘서 초기화
  * 파라미터가 있는 생성자를 만들면 기본 생성자는 추가되지 않음!!

<br>

---

<br>

## this

#### `this.`

* 참조 변수로써 객체 자신을 가리킴
  * `this`를 이용해 자신의 멤버에 접근 가능
* **객체에 대한 참조**
  * 따라서 `static` 영역에서 `this` 사용 불가

* 용도
  * 로컬 변수와 멤버 변수의 이름이 동일할 경우
    * 멤버 변수임을 명시적으로 나타냄

#### `this()`

* 메서드와 마찬가지로 생성자도 오버로딩 가능

* 필요성

  * 객체 생성 시 필요한 멤버변수만 초기화 진행하고 싶을 때
  * 생성자 별 코드의 중복 발생

* 한 생성자에서 다른 생성자를 호출할 때 사용

* 반드시 첫 줄에서만 호출 가능

* 예시

  * `this()` 사용 안했을 때

    ```
    public class OverloadConstructorTest {
    	String name = "아무개";
    	int ange = 0;
    	
    	OverloadConstructorTest(String name, int age) {
    		this.name = name;
    		this.age = age;
    	}
    	
    	OverloadConstructorTest(String name) {
    		this.name = name;
    	}
    	
    	OverloadConstructorTest() {
    		this.name = "홍길동";
    		this.age = 100;
    	}
    }
    ```

  * `this()` 사용했을 때

    ```java
    public class OverloadConstructorTest {
    	String name = "아무개";
    	int ange = 0;
    	
    	OverloadConstructorTest(String name, int age) {
    		this.name = name;
    		this.age = age;
    	}
    	
    	OverloadConstructorTest(String name) {
    		this(name, 0);
    	}
    	
    	OverloadConstructorTest() {
            // 첫 번째 라인에서만 사용 가능
    		this("홍길동", 100);
    	}
    }
    ```

<br>

---

<br>

## String

#### 비교

`str.equals("##")`

#### 공백 제거

`str.trim()`

<br>

---

<br>

## 클래스의 Set/Get

> private 멤버 변수 다루기

* 이클립스에서 자동으로 생성하기
  * [Source] - [Generate Getters and Setters] 

<br>

---

<br>

## static

* **static**
  * `클래스명.XXX`으로 static 붙은 멤버변수, 함수 접근 가능
* **public**
  * `public`을 붙여줘야 외부에서도 사용 가능

```java
public class Calc{
	public static double PI = 3.14;
	
	public static int circle(int r){
		return r*r;
	}
}
```

```java
System.out.println(Calc.circle(5)*Calc.PI)
```



---

