# OOP (3)

<br>

---

<br>

## 추상 클래스

* 클래스들의 공통 분모를 뽑아 상속 구조를 만들자...

* 자손클래스에서 반드시 재정의해서 사용되지만, 조상의 구현이 무의미한 메서드가 생길 것임.

  * 메서드의 선언부만 남기고 구현부는 세미클론(`;`)으로 대체
  * 구현부가 없다는 의미로 `abstract` 키워드를 메서드 선언부에 추가
  * 객체를 생성할 수 없는 클래스라는 의미로 클래스 선언부에 `abstract`를 추가

  ```java
  abstract class Vehicle {
  	private int curX, curY;
  	
  	public void reportPosition() {
  		system.out.printf("현재 위치: (%d, %d)%n", curX, curY);
  	}
  	
  	public abstract void addFuel();
  }
  ```

<br>

#### abstract 클래스

* 상속 전용의 클래스

  * 클래스에 구현부가 없는 메서드가 있으므로 **객체를 생성할 수 없음**
  * 하지만 상위 클래스 타입으로써 **자식을 참조할 수는 있음**

  ```java
  Vehicle v = new Vehicle(); // X
  vehicle v = new DeselSUV(); // O
  ```

* 조상 클래스에서 상속받은 `abstract` 메서드를 재정의 하지 않은 경우

  * 클래스 내부에 abstract 메서드가 있는 경우이므로 자식 클래스는 abstract 클래스로 선언되어야 함

<br>

#### 추상 클래스를 사용하는 이유

* 구현의 강제를 통해 프로그램의 안정성 향상
* interface에 있는 메서드 중 구현할 수 있는 메서드를 구현해 개발의 편의 지원

<br>

---

<br>

## Interface

> 서로 다른 두 시스템 장치, 소프트웨어 따위를 서로 이어 주는 부분. 또는 그런 접속 장치

* GUI
  * Graphic User Interface
  * 프로그램과 사용자 사이의 접점

<br>

#### 인터페이스 작성

* 최고 수준의 추상화 단계

  * 모든 메서드가 abstract 형태
    * JDK 8 에서 `default method`와 `static method` 추가

* 형태

  * 클래스와 유사하게 `interface` 선언

  * 멤버 구성

    * **모든 멤버변수**는 `pubilc static final`이며 생략 가능
    * **모든 메서드**는 `public abstract`이며 생략 가능

    ```java
    public interface MyInterface {
    	public static final int MEMBER1 = 10; // 생략하지 않고 썼을 때
    	int MEMBER2 = 10; // 생략했을 때
    	
    	public abstract void method1(int param); // 생략하지 않고 썼을 때
    	void method2(int param); // 생략했을 때
    }
    ```

<br>

#### 인터페이스 상속

* `extends`를 이용해 상속 가능
* 클래스와 다른점
  * 인터페이스는 **다중 상속**이 가능
  * `extends xxx1, xxx2, ...`

<br>

#### 인터페이스 구현과 객체 참조

* 클래스에서 `implements` 키워드를 사용해서 interface 구현
* `implements` 한 클래스
  * **모든 abstract 메서드를 override해서 구현하거나**
  * 구현하지 않을 경우 abstract 클래스로 표시해야 함
* 여러 개의 interface implements 가능

* **다형성**은 조상 클래스 뿐 아니라 조상 인터페이스에도 적용 ★★★
* `instanceof`로 인터페이스 상속여부 확인 가능!

<br>

#### 인터페이스의 필요성

* 구현의 강제로 표준화 처리
  * `abstract` 메서드 사용
  * 손쉬운 모듈 교체 지원
* **서로 상속 관계가 없는 클래스**에게 **인터페이스를 통한 관계 부여로 다형성 확장**
* 모듈 간 독립적 프로그래밍 가능
  * 개발 기간 단축

* JAVA Application 와 SQL의 Interface
  * **JDBC**
  * SQL별 interface 구현

<br>

#### default method

* 인터페이스에 선언 된 **구현부가 있는 일반 메서드**
  * `abstract` 필요 없음!!
* 메서드 선언부에 `default modifier` 추가 후 메서드 구현부 작성
  * 접근 제한자는 `public`으로 한정됨 (생략 가능)
* **필요성**
  * 기존에 interface 기반으로 동작하는 라이브러리의 interface에 추가해야 하는 기능이 발생
  * 기존 방식으로라면 모든 구현체들이 추가되는 메서드를 override 해야 함
  * **default 메서드**는 **abstract가 아니므로 반드시 구현 해야 할 필요는 없어짐**

* **충돌**
  * JDK 1.7 이하의 java에서는 `interface method`에 구현부가 없으므로 충돌이 없었음
  * 1.8부터 `default method`가 생기면서 동일한 이름을 갖는 구현부가 있는 메서드가 충돌
  * method 우선순위
    * `super class`의 method 우선
      * **super class가 구체적인 메서드를 갖는 경우** default method는 무시됨
    * interface간의 충돌
      * 하나의 interface에서 default method를 제공하고 다른 interface에서도 같은 이름의 메서드(default 유무와 무관)가 있을 때 **sub class는 반드시 override 해서 충돌 해결!!**

<br>

#### static method

* interface에 선언된 static method
* 일반 static 메서드와 마찬가지로 별도의 객체가 필요 없음
* 구현체 클래스 없이 바로 인터페이스 이름으로 메서드에 접근해서 사용 가능

<br>

---

<br>

## Generics

* 다양한 타입의 객체를 다루는 메서드
* 컬렉션 클래스에서 **컴파일 시에 타입 체크**
* 미리 사용할 타입을 명시해서 형 변환을 하지 않아도 되게 함
  * 객체 타입에 대한 안전성 향상 및 형 변환의 번거로움 감소

<br>

#### 표현

* 클래스 또는 인터페이스 선언시 `<>`에 타입 파라미터 표시

  ```java
  public class Class_Name<T> {}
  public interface Interface_Name<T> {}
  ```
  * Class_Name : Raw Type
  * Class_Name<T> : Generic Type

* 타입 파라미터

  * 특별한 의미의 알파벳 보다는 단순히 **임의의 참조형 타입**을 말함
  * T : reference Type
  * E : Element
  * K : Key
  * V : Value

* 객체 생성
  * 변수 쪽과 생성 쪽의 타입은 반드시 같아야 함

<br>

#### 클래스 생성

* 담을 떄는 편하지만 뺼 떄는 번거로움

  ```java
  class NormalBox {
  	private Object some;
  	
  	public Object getSome() {
  		return some;
  	}
  	
  	public void setSome(Object some) {
  		this.some = some;
  	}
  }
  ```

  * `instanceof`
  * 타입 체크 해야함

* 담을 때는 번거롭지만 뺼 떄는 편하다

  ```java
  class GenericBox<T> {
  	private T some;
  	
  	public T getSome() {
  		return some;
  	}
  	
  	public void setSome(T some) {
  		this.some = some;
  	}
  }
  ```

  * `GenericBox<String> gbox = new GenericBox<>();`
  * 타입 체크 하지 않아도 됨

<br>

#### type parameter의 제한

* 필요에 따라 구체적인 타입 제한 필요

* `class Class_Name <T extends Number>`

  ```java
  class class_Name <T extends Integer>
  ```

  * `Integer`로 제한

* 인터페이스로 제한할 경우도 `extends` 사용

* 클래스와 함께 인터페이스 제약 조건을 이용할 경우 `&`로 연결

  ```java
  class Class_Name<T extends XXX1 & XXX2 & XXX<String>> {}
  ```

<br>

#### Generic Method

* 파라미터와 리턴타입으로 type parameter를 갖는 메서드

* 메서드 리턴 타입 앞에 타입 파라미터 변수 선언

  ```
  public <P> void method(P p) {}
  ```

* 타입 결정 시점
  * 객체 생성 시점에 `T`의 타입 결정
  * **메서드 호출 시점**에 `P`의 타입 결정

* `XXX.<Long>method(20L)`

