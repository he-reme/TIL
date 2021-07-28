# Exception

> 예외

<br>

---

<br>

## 에러와 예외

* 어떤 원인에 의해 오동작 하거나 비정상적으로 종료되는 경우
* 심각도에 따른 분류
  * **Error**
    * 메모리 부족, stack overflow와 같이 일단 발생하면 복구할 수 없는 상황
    * 프로그램의 비 정상적 종료를 막을 수 없음 → 디버깅 필요
  * **Exception**
    * 읽으려는 파일이 없거나 네트워크 연결이 안 되는 등 수습될 수 있는 비교적 상태가 약한 것들
    * 프로그램 코드에 의해 수습할 수 있는 상황
* **exception handing (예외처리)**
  * 예외 발생 시 프로그램의 비 정상 종료를 막고 정상적인 실행 상태를 유지하는 것
  * 예외의 감지 및 예외 발생 시 동작할 코드 작성 필요

<br>

#### 예외 클래스의 계층

* Error 계열
  * `Error`
    * `OutOfMemoryError`
* Checked exception 계열
  * checked exception : 예외에 대한 대처 코드가 없으면 컴파일이 진행되지 않음
  * `Exception`
    * `SQLException`
    * `IOException`
      * `FileNotFoundException`

* Unchecked exception 계열
  * RuntimeException의 하위 클래스
  * unchecked exception : 예외에 대한 대처 코드가 없더라도 컴파일은 진행됨
  * `Exception`
    * `RuntimeException`
      * `ArithmeticException`

<br>

---

<br>

## exception handling 기법

#### try ~ catch 구문

```java
try {
	// 예외가 발생할 수 있는 코드
	// 이때 JVM의 동작
} catch(XXExeption e) {
	// 예외가 발생했을 때 처리할 코드
}
```
* try : **JVM 동작** → 예외 발생 → new XXException → 받아라! throw!!
* catch : 던진 예외를 받음

<br>

#### Exception 객체의 정보 활용

* Throwable의 주요 메서드
  * `public String getMessage()`
    * 발생된 예외에 대한 구체적인 메시지를 반환
  * `public Throwable getCause()`
    * 예외의 원인이 되는 Throwable 객체 또는 null을 반환
  * `public void printStackTrace()`
    * 예외가 발생된 메서드가 호출되기까지의 메서드 호출 스택을 출력한다.
    * 디버깅의 수단으로 주로 사용된다
    * `e.printStackTrace()`

<br>

#### try-catch문에서의 흐름

* **try 블록에서 예외가 발생하면**
  * JVM이 해당하는 Exception 클래스의 객체 생성 후 던짐 (throw)
    * throw new XXException()
    * 딱 예외가 발생한 코드에서 바로 catch 블록으로 넘어감
  * 던져진 exception을 처리할 수 있는 catch 블록에서 받은 후 처리
    * 적당한 catch 블록을 만나지 못하면 예외처리는 실패
  * 정상적으로 처리되면 try-catch 블록을 벗어나 다음 문장 실행
* **try 블록에서 어떠한 예외도 발생하지 않은 경우**
  * catch문을 거치지 않고 try-catch블록의 다음 흐름 문장을 실행

<br>

#### 다중 exception handling

* try 블록에서 여럴 종류의 예외가 발생할 경우

  * 하나의 try 블록에 여러 개의 catch 블록 추가 가능

  * 예외 종류별로 catch 블록 구성

    ```java
    try {
    
    } catch(XXException e) {
    
    } catch(YYException e) {
    
    } catch(Exception e) {
    
    }
    ```

    * `Exception` 
      * Exception들의 조상
      * 위에서 해당 안하면 여기서 처리
      * switch의 default라고 생각하면 됨

* 다중 catch 문장 작성 순서 유의사항

  * JVM이 던진 예외는 catch 문장을 찾을 때는 다형성이 적용됨
  * 상위 타입의 예외가 먼저 선언되는 경우 뒤에 등장하는 catch 블록은 동작할 기회가 없음
  * 상속 관계가 없는 경우는 무관
  * 상속 관계에서는 **작은 범위(자식)에서 큰 범위(조상)순**으로 정의8

* 다중 예외 처리를 이용한 Checked Exception 처리

  * 발생하는 예외들을 하나로 처리하기
    * 예외상황 별 처리가 쉽지 않음
    * 가급적 예외 상황 별로 처리하는 것을 권장
  * 심각하지 않은 예외를 굳이 세분화해서 처리하는 것도 낭비

  ▶ 계층을 이루는 예외 처리

<br>

#### try ~ catch ~ finally

* **finally**는 예외 발생 여부와 상관 없이 언제나 실행

  * 중간에 return을 만나는 경우도 finally 블록을 먼저 수행 후 리턴 실행

  ```java
  try {
  
  } catch(XXException) {
  
  } finally{
  	// try block에서 접근했던 System자원의 안전한 원상 복구
  }
  ```

* **finally** 주요 목적 : try블록에서 사용한 리소스 반납

  * 생성한 시스템 자원을 반납하지 않으면 장래 resource leak 발생 가능 → close 처리

* **finally에서 자원 정리**

  * close이용한 자원 정리
    * 지저분해 보임

* **try with resources**

  * JDK 1.7 이상에서 리소스의 자동 close 처리

    ```java
    try(리소스타입1 res1 = 초기화; 리소스타입2 res2 = 초기화; ...){
    } catch(Exception e){
    
    }
    ```

    * res1, res2 모두 자동 close 처리됨.

  * try 선언문에 선언된 객체들에 대해 자동 close 호출

    * 단 해당 객체들이 AutoCloseable Interface 구현할 것
      * 각종 I/O stream, socket, connection
    * 해당 객체는 try블록에서 다시 할당될 수 없음

<br>

---

<br>

## throws 키워드를 통한 처리 위임

* method에서 처리해야 할 하나 이상의 예외를 **호출한 곳으로** 전달 (처리 위임)

  * 예외가 없어지는 것이 아니라 단순히 전달됨

  * 예외를 전달 받은 메서드는 다시 예외 처리의 책임 발생

    ```java
    void exceptionMethod() thorws Exception1, Exception2... {
    	// 예외 발생 코드
    }
    
    // 예외 처리 책임
    void methodCaller() {
    	try{
    		exceptionMethod();
    	} catch(Exception e) {
    	
    	}
    }
    ```
    * 예외처리 책임은 try - catch 문에서!!

  * 처리하려는 예외의 조상 타입으로 throws 처리 가능

<br>

#### checked exception과 throws

* checked exception은 반드시 try~catch 또는 throws 필요
* 필요한 곳에서 try~catch 처리

<br>

#### Runtime exception과 throws

* runtime exception은 throws 하지 않아도 전달되지만
* 결국은 try~catch로 처리해야 함

<br>

#### 로그 분석과 예외의 추적

* Throwable의 printStackTrace는 메서드 호출 스택 정보 조회 가능
  * 최초 호출 메서드에서부터 예외 발생 메서드까지의 스택 정보 출력

* 꼭 확인해야할 정보

  * 예외 종류 : 어떤 예외인가?
  * 예외 원인 : 예외 객체의 메시지는 무엇인가?
  * 디버깅 출발점 : 어디서 발생했는가?
    * 직접 작성한 코드를 디버깅 대상으로!
    * 참조하는 라이브러리(java.xx등)는 과감히 건너뛰기

  * 예시
    * `java.lang.ClassNotFoundException : Some Class`
    * 예외 종류 : java.lang.ClassNotFoundException 
    * 예외 확인 : Some Class
    * 디버깅 출발점 : 에러코드 쭈루루루룩 나왔을 때, 직접 작성한 코드중 맨 위에 있는 부분

<br>

#### throws의 목적과 API 활용

* API가 제공하는 많은 메서드들은 사전에 예외가 발생할 수 있음을 선엄부에 명시하고 프로그래머가 그 예외에 대처하도록 강요함
* Java API가 예외 발생, 예외 처리해버리면 개발자는 상황을 인지하지 못함...
* 그래서 Java API가 예외 발생하면 예외 전파함! 이렇게 하게되면 개발자는 상황을 인지하고 적절한 예외처리를 할 수 있는 것임!

<br>

#### 메서드 재정의와 throws

* 메서드 재정의 시 조상 클래스 메서드가 던지는 예외보다 부모예외를 던질 수 없음

  * 부모가 치지 않은 사고를 자식이 칠 수 없음.

  ```java
  Class Parent {
  	void method A() throws IOException{}
  	void method b() throws ClassNotFoundException{}
  }
  public OverridingTest extends Parent {
  	@Override
  	void methodA() throws FileNotFoundException{
  	
  	}
  	
  	@Override
  	void methodB() throws Exception{
  	
  	}
  }
  ```

  * 잘못된 부분은?

    * `methodB`

    * 부모 클래스가 던지는 예외(`ClassNotFoundException`) 보다 더 부모를 던짐(`Exception`) 

<br>

---

<br>

## 사용자 정의 예외

* API에 정의된 exception이외에 필요에 따라 사용자 정의 예외 클래스 작성
* 대부분 Exception 또는 RuntimeException 클래스를 상속받아 작성
  * checked exception 활용 : 명시적 예외 처리 또는 thorws 필요
  * runtime exception 활용 : 묵시적 예외 처리 가능
* 사용자 정의 예외를 만들어 처리하는 장점
  * 객체의 활용 - 필요한 추가정보, 기능 활용 가능
  * 코드의 재사용 - 동일한 상황에서 예외 객체 재사용 가능
  * throws 메커니즘 이용 - 중간 호출 단계에서 return 불필요

<br>

---

<br>

## RuntimeException

* 많은 경우 시스템의 RuntimeException은 처리의 대상이기 보다는 디버깅의 대상이다!
* try-catch보다는 if문으로 처리!!