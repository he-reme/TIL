# Spring Framework

> DI : Dependency Injection

#### Spring Framework?

* 엔터프라이즈 급 애플리케이션을 만들기 위한 모든 기능을 종합적으로 제공하는 경량화 된 솔루션
* JEE (Java Enterprise Edition) 가 제공하는 다수의 기능을 지원하고 있기 때문에, JEE를 대체하는 Framework로 자리잡고 있음
* SpringFramework는 JEE가 제공하는 다양한 기능을 제공하는 것 뿐만 아니라, DI (Dependency Injection)나 AOP(Aspect Oriented Programming)와 같은 기능도 지원함
* Spring Framework는 자바로 Enterprise Application을 만들 때 포괄적으로 사용하는 Programming 및 Configuration Model을 제공해주는 Framework로, Application 수준의 인프라 스트럭쳐를 제공
* 즉, 개발자가 복잡하고 실수하기 쉬운 Low Level에 신경쓰지 않고 Business Logic 개발에 전념할 수 있도록 해줌

<br>

---

<br>

## Spring Framework 구조

#### Spring 삼각형

* Enterprise Application 개발 시 복잡함을 해결하는 Spring의 핵심
  1. POJO
     * Plain Old Java Object
     * 특정 환경이나 기술에 종속적이지 않은 객체지향 원리에 충실한 자바객체
     * 테스트하기 용이하며, 객체지향 설계를 자유롭게 적용할 수 있음
  2. PSA
     * Portable Service Abstraction
     * 환경과 세부기술의 변경과 관계없이 일관된 방식으로 기술에 접근할 수 있게 해주는 설계 원칙
  3. IoC/DI ★★★
     * Dependency Injection
     * IoC는 제어의 역전
       * DI : 그냥 가져다 줌
       * DL : 필요한 시점에 lookup
     * DI는 유연하게 확장 가능한 객체를 만들어 두고 객체 간의 의존 관계는 외부에서 다이나믹하게 설정
  4. AOP
     * Aspect Oriented Programming
     * 관심사의 분리를 통해서 소프트웨어의 모듈성을 향상
     * 공통 모듈을 여러 코드에 쉽게 적용 가능



