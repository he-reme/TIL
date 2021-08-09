# OOP

> 객체지향 언어
>
> OOP is A P.I.E

#### 객체지향 언어의 특징

* Abstraction
  * 추상화
  * 현실의 객체를 추상화해서 클래스를 구성한다
* Polymorphism
  * 다형성
  * 하나의 객체를 여러 가지 타입(형)으로 참조할 수 있다
* Inheritance
  * 상속
  * 부모 클래스의 자산을 물려받아 자식을 정의함으로 코드의 재사용이 가능하다
* Encapsulation
  * 데이터 은닉과 보호
  * 데이터를 외부에 직접 노출시키지 않고 메서드를 이용해 보호할 수 있다

<br>

---

<br>

## 1. Inheritance

> 상속

* 기존 클래스의 자산(멤버)을 자식 클래스에서 재사용하기 위한 것

  * 부모의 생성자와 초기화 블록은 상속하지 않는다

* 기존 클래스의 멤버를 물려 받기 때문에 코드의 절감

  * 부모의 코드를 변경하면 모든 자식에게도 적용
  * 유지 보수성 향상

* 상속의 적용

  * extends 키워드 사용

    ```java
    public class Person{
    	String name;
    	
    	void eat(){}
    	void jump(){}
    }
    ```

    * Person의 멤버 : 3개

    ```java
    public class SpiderMan extends Person {
    	boolean isSpider;
    	void fireWeb(){}
    }
    ```

    * SpiderMan의 멤버 : 5개

* 클래스 다이어그램에서...

  * 실선 화살표 방향

    ```java
    SpiderMan → Person
    ```

    * SpiderMan이 Person을 상속받고 있다.
    * Person 클래스
      * 조상 클래스, 부모 클래스, 상위 클래스, 슈퍼 클래스
    * Spiderman 클래스
      * 자식 클래스, 부모 클래스 , 상위 클래스, 서브 클래스

* 상속의 관계는 `is a` 관계라고 함

  * Person is a Object
  * SpiderMan is a Person

<br>

#### Object 클래스

* 가장 최상위 클래스로,, 모든 클래스의 조상

* 모든 클래스의 조상 클래스
  * 별도의 `extends` 선언이 없는 클래스들은 `extends Object`가 생략됨
  * 따라서 모든 클래스에는 Object 클래스에 정의된 메서드가 있음
* `java.lang.Object`
  * `java.lang` : JRE에서 배포되는 시스템 라이브러리에 포함되어있음
* 예
  * `Object.toString()` 같은 메소드 사용 가능

<br>

#### 단일 상속

* 다중 상속의 경우
  * 여러 클래스의 기능을 물려받을 수 있으나 관계가 매우 복잡해짐
  * 예) 동일한 이름의 메서드가 두 부모에게 있다면 자식은 어떤 메서드를 쓸 것인가?
* **자바는 단일 상속만 지원!!**
  * 대신 `interface`와 `포함 관계(has a)`로 단점 극복

<br>

#### 포함 관계

* 상속 이외에 클래스를 재활용 하는 방법

  * 2개 이상의 클래스에서 특성을 가져올 때 하나는 상속, 나머지는 멤버 변수로 처리

  *  `has a` 관계

    ```java
    public class SpiderMan extends Person {
    	Spider spider;
    	boolean isSpider;
    	
    	void fireWeb() {
    		if(isSpider) {
    			spider.fireWeb();
    		}else {
    			System.out.println("Person은 거미줄 발사 불가");
    		}
    	}
    }
    ```

    * 상속 : `Person`
    * 포함(멤버변수) : `Spider`

* 포함 관계의 UML 표현 : 실선

* Spider 코드를 수정하면 SpiderMan에도 반영되므로 유지 보수성 확보

<br>

#### 메서드 오버라이딩

* 조상 클래스에 정의된 메서드를 자식 클래스에서 적합하게 수정하는 것

* 오버로딩과 구분!!!!
  * 오버 로딩은 메서드 이름이 같고, 매개변수만 다르다
* 오버라이딩의 조건
  * 메서드 이름이 같아야 한다
  * 매개 변수의 개수, 타입, 순서가 같아야 한다
  * 리턴 타입이 같아야 한다
  * 접근 제한자는 부모 보다 범위가 넓거나 같아야 한다
  * 조상보다 더 큰 예외를 던질 수 없다

<br>

#### Annotation

* 주석
* 메서드 오버라이딩 한 메서드 위에 적음
* 컴바일러, JVM, 프레임워크 등이 보는 주석
* 소스코드에 메타 데이터를 삽입하는 형태
  * 소스코드에 붙여놓은 라벨
  * 코드에 대한 정보 추가
    * 소스 코드의 구조 변경, 환경 설정 정보 추가 등의 작업 진행
* JDK 1.5 의 기본 annotation의 예
  * `@Deprecated`
    * 컴파일러에게 해당 메소드가 deprecated 되었다고 알려줌
    * 안쓰는게 좋겠어~ 라고 알림
  * `@Override`
    * 컴파일러에게 해당 메서드는 override한 메서드 임을 알려줌
    * `@Override`가 선언된 경우 반드시 super class에 선언되어있는 메서드여야 함
    * 오버라이드 가능 여부를 확인해주고, 안되는 애는 에러 메시지를 띄워줌 → 실수한 것을 확인할 수 있음
  * `@SupperessWarnings`
    * 컴파일러에게 사소한 warning의 경우 신경 쓰지 말라고 알려줌

<br>

#### `super` 키워드

* `this`를 통해 멤버에 접근했듯이 **`super`를 통해 조상 클래스 멤버 접근**

* `super.`를 이용해 조상의 메서드 호출로 조상의 코드 재사용

* 변수의 scope

  * 사용된 위치에서 점점 확장해가며, 처음 만난 선언부에 연결됨
  * method 내부 → 해당 클래스 멤버 변수 → 조상 클래스 멤버 변수

  ```java
  class Parent {
  	String x = "parent";
  }
  
  class Child extends Parent {
  	String x = "child";
  	
  	void method() {
  		String x = "method";
  		System.out.println("x: "+x);
  		System.out.println("this.x: "+this.x);
  		System.out.println("super.x: "+super.x);
  	}
  }
  
  public class ScopeTest{
  	public static void main(String[] args) {
  		Child child = new Child();
  		child.method();
  	}
  }
  ```

  * 문제

    1. 현재 상태에서 출력 결과

       "method child parent"

    2. method의 x를 주석하면?

       "child child parent"

    3. child의 x를 주석하면?

       "parent parent parent"

* `this()`가 해당 클래스의 다른 생성자를 호출하듯 `super()`는 조상 클래스의 생성자 호출

  * 조상 클래스에 선언된 멤버들은 조상 클래스의 생성자에서 초기화가 이뤄지므로 이를 재사용
  * 자식 클래스에 선언된 멤버들만 자식 클래스 생성자에서 초기화

* `super()`는 자식 클래스 생성자의 맨 첫 줄에서만 호출 가능

  * 즉 생성자의 첫 줄에만 `this()` 또는 `super()`가 올 수 있다.

* 명시적으로 `this()` 또는 `super()`를 호출하지 않는 경우 컴파일러가 `super()` 삽입

  * 결론적으로 맨 상위의 Object까지 객체가 만들어지는 구조

  ```java
  class Person {
  	String name;
  	Person(String name) {
  		// super(); // Object의 기본 생성자 호출
  		this.name = name;
  	}
  }
  ```

* `static`은 this와 super키워드 사용 불가... 메모리 영역이 다르기 때문에

  * `main` 에서도 사용 불가

<br>

---

<br>

## Object 클래스

#### `toString` 메서드

* 객체를 문자열로 변경하는 메서드

* Object의 메서드는 주소값을 출력해줌

  ```java
  public String toString() {
  	return getClass().getName() + "0" + Integer.toHexString(hashCode());
  }
  ```

  * 이는 우리가 원하는 기능은 아님

* 오버라이딩 해서 사용!!!

* [source] - [generate toString] 으로 자동 생성 가능

<br>

---

<br>

## 2. Encapsulation

> 데이터 은닉과 보호

* 정보를 보호하기 위한 대책은?
  * 변수
    * `private` 접근으로 막기
  * 공개되는 메서드를 통한 접근 통로 마련
    * `setter / getter`
    * 메서드에 정보 보호 로직 작성

<br>

#### 객체 생성 제어와 Singleton 디자인패턴

* 객체의 생성을 제한해야하는 경우는?

  * 여러 개의 객체가 필요 없는 경우
    * = 수정 가능한 멤버 변수가 없고 기능만 있는 경우
    * 이런 객체를 stateless한 객체라고 함
  * 객체를 계속 생성/삭제 하는데 많은 비용이 들어서 재사용이 유리한 경우

  * 이러한 경우는 Singleton 디자인 패턴 적용!!

* **Singleton 디자인 패턴**

  * 외부에서 생성자에 접근 금지 → 생성자의 접근 제한자를 private로 설정
  * 내부에서는 private에 접근 가능하므로 직접 객체 생성 → 멤버 변수이므로 **private** 설정
  * 외부에서 private member 접근 가능한 **getter 생성** → setter는 불필요 
  * 객체 없이 외부에서 접근할 수 있도록 **getter와 변수에 static 추가**
  * 외부에서는 언제나 getter를 통해서 객체를 참조하므로 **하나의 객체 재사용**

  ```java
  public class Teacher {
  	
  	// 나만 만들 수 있음.
  	private static Teacher t = new Teacher();
  	
  	// 외부에서 생성 불가
  	private Teacher() {}
  	
  	// 이걸 통해서 가져다써~
  	public static Teacher getTeacher() {
  		return t;
  	}
  }
  ```

  ```java
  public class TeacherTest {
  
  	public static void main(String[] args) {
  
  		Teacher t1 = Teacher.getTeacher();
  		
  		Teacher t2 = Teacher.getTeacher();
  		
  		System.out.println(t1==t2); // true
  	}
  }
  ```

<br>

---

<br>

## 3. Polymorphism

> 다형성
>
> OPP의 꽃..!

* 하나의 객체가 많은 형(타입)을 가질 수 있는 성질

#### 정의

* **상속 관계**에 있을 때 **조상 클래스의 타입으로 자식 클래스 객체를 레퍼런스** 할 수 있다.

<br>

#### 예시

* 상속 관계 : Venom → SpiderMan → Person → Object

  ```java
  SpideraMan onlyOne = new SpiderMan();
  SpiderMan sman = onlyOne; // 참조 가능
  Person person = onlyOne; // 참조 가능 
  Object obj = onlyOne; // 참조 가능 
  Venom venom = onlyOne; // 참조 불가능
  ```
  * 참조 가능 : 부모 클래스이므로 참조 가능

<br>

#### 활용 예

1. 다른 타입의 객체를 다루는 배열

   * 배열의 특징 : 같은 타입의 데이터를 묶음으로 다룬다
   * 다형성으로 다른 타입의 데이터를 하나의 배열로 관리

   ```java
   void poly(){
   	Person[] persons = new Person[10];
   	persons[0] = new Persion();
   	persons[0] = new SpiderMan();
   }
   ```

2. 매개 변수의 다형성

   * 메서드가 호출되기 위해서는 메서드 이름과 파라미터가 맞아야 함

     * 그럼 `println`은?

       ```java
       public void println(Object x) {
       	String s = String.valueOf(x);
       	syncronized(this) {
       		print(s);
       		newLine();
       	}
       }
       ```

       * `Object`가 소화!!
       * 조상을 파라미터로 처리한다면 객체 타입에 따라 메서드를 각각 만들 필요가 없어짐

   * API에서 파라미터로 `Object`를 받는다는 것은 모든 객체를 처리한다는 말임.

   * 물론 필요하다면 하위 클래스에서 오버라이딩 필요

<br>

#### Object는 모든 클래스의 조상!

* Object 배열은 어떤 타입의 객체라도 다 저장할 수 있음

* 자바의 자료 구조를 간단하게 처리할 수 있음
  * 이와 같은 특성을 이용하여 **Collection API**가 등장하게 됨
  * 기본형은 담을 수 있을까?

<br>

#### 다형성과 참조형 객체의 형 변환

* 메모리에 있는 것과 사용할 수 있는 것의 차이

  ```
  Person person = new SpiderMan();
  ```

  * 메모리에 있더라도 참조하는 변수의 타입에 따라 접근할 수 있는 내용이 제한됨
  * `SpiderMan()`이 메모리에 있지만.. `Person`타입이 참조하고 있기 때문에.. `SpiderMan` 클래스에만 있는 멤버는 접근 불가

* 참조형 객체의 형 변환
  * 묵시적 캐스팅 : child → super
  * 명시적 캐스팅 : super → child

* 부적절한 형변환

  ```java
  Person person = new Persion();
  SpiderMan sman = (SpiderMan) person;
  ```

  * 메모리에 있는 것도 Person형이기 때문에 부적절한 형변환임.

  * 적절한 형변환

    ```java
    Person person = new SpiderMan();
    SpiderMan sman = (SpiderMan) person;
    ```

* `instanceof` 연산자

  * 실제 메모리에 있는 객체가 특정 클래스 타입인지를 `boolean`으로 리턴
  * 조상을 무작정 자손으로 바꿀 수 없기 때문에 확인하는 방법

  ```java
  Person person = new Person();
  
  // 클래스 타입 확인
  if(person instanceof Spiderman) {
  	Spiderman sman = (SpiderMan) person;
  }
  ```

  * 형변환할 클래스타입과 메모리에 있는 클래스타입이 동일하면 형변환~

<br>

#### 참조 변수의 레벨에 따른 객체의 멤버 연결

* SuperClass

  ```java
  class SuperClass {
  	String x = "super";
  	public void method() {
  		System.out.println("super class method");
  	}
  }
  ```

* SubClass

  ```java
  class SubClass extends SuperClass {
  	String x = "sub";
  	public void method() {
  		System.out.println("sub class method");
  	}
  }
  ```

* 실행

  ```java
  public class Test {
  	public static void main(String[] args) {
  		SubClass subClass = new SubClass();
  		System.out.println(subClass.x); // "sub"
  		subClass.method(); // "sub class method"
  		
  		SuperClass superClass = subClass;
  		System.out.println(superClass.x); // "super"
  		superClass.method(); // "sub class method"
  	}
  }
  ```

* **상속 관계에서 객체의 멤버 변수가 중복될 때**
  * 참조 변수의 타입에 따라 연결이 달라짐
* **상속 관계에서 객체의 메서드가 중복될 때 (메서드가 override 되었을 때)**
  
  * 무조건 자식 클래스의 메서드가 호출됨
  * 최대한 메모리에 생성된 실제 객체에 최적화 된 메서드가 동작함
* 실제 사용
  * 상위로(자식으로) 올라갈 수록 활용도도 높아짐
    * 하지만 코드의 복잡성도 함께 증가
  * Java API처럼 공통 기능인 경우 Object를 파라미터로 쓰겠지만
    * 많은 경우 비즈니스 로직 상 최상위 객체 사용 권장

* 예시 : 객체가 출력되는 과정

<br>

#### 객체가 출력되는 과정

* `System.out.print(Object obj)`를 이용한 객체 출력

  ```java
  SuperClass superClass = new SubClass();
  System.out.print(SuperClass);
  ```

* PrintStream의 `print` 메서드

  ```java
  public void print(Object obj) {
  	write(String.valueOf(obj));
  }
  ```

* String의 ValueOf

  ```java
  public static String valueOf(Object obj) {
  	return (obj == null) ? "null" : obj.toString();
  }
  ```

* Object의 toString

  ```java
  public String toString() {
  	return getClass().getName() + "@" + Integer.toHexString(hashCode());
  }
  ```

* 객체가 출력되는 건 결국 Object의 toString 때문이었다!!

<br>

#### 완전 중요한 예시

```java
class Person{
	String name = "Person name 변수";
	Person(){
		System.out.println("Person 생성자");
	}
	void eat(){}
	void jump(){}
	public void methodTest() {
		System.out.println("Person 메소드");
	}
}

class SpiderMan extends Person {
	boolean isSpider;
	String name = "SpiderMan name 변수";
	
	SpiderMan(){
		System.out.println("Spiderman 생성자");
	}
	
	public void methodTest() {
		System.out.println("Spiderman 메소드");
	}
	void fireWeb(){}
}

public class Test {

	public static void main(String[] args) {
		Person sm = new SpiderMan();
		System.out.println("--------------------------");
		
		System.out.println(sm.name);
		sm.methodTest();
		System.out.println("--------------------------");
		
		SpiderMan sm1 = (SpiderMan) sm;
		System.out.println(sm1.name);
		sm1.methodTest();
	}
}
```

* 출력

  ```
  Person 생성자
  Spiderman 생성자
  --------------------------
  Person name 변수
  Spiderman 메소드
  --------------------------
  SpiderMan name 변수
  Spiderman 메소드
  ```

  * 상속 관계에서 **객체의 멤버 변수가 중복될 때**
    * 참조 변수의 타입에 따라 연결이 달라짐
  * 상속 관계에서 **객체의 메서드가 중복될 때** (메서드가 override 되었을 때)
    * 무조건 자식 클래스의 메서드가 호출됨

<br>

