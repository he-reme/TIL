# Start Camp (1)

> 환경설정 및 프로젝트 생성해보기

#### 설치

1. zulu8.33.0.1-jdk8.0~~
   * jdk 설치 및 환경 변수 설정
2. STS.exe
   * Spring Tool Suite 설치
3. apache tomcat
   * STS - Open Perspective - JAVA EE - server  탭 - New Server - [Apache] - [Tomcat v9.0 Server] - Next - Browse - `C:\SSAFY\apache-tomcat-9.0.50`
   * tomcat server 더블클릭
     * HTTP/1.1 포트 → 9000 으로 변경
     * 충돌 날까봐
   * 그 후 프로젝트 생성~~

<br>

#### STS.ini

* STS 설정하기
* 내 컴퓨터 사양에 따라 변동줘도 됨

* ```
  -Xms256m
  -Xmx1024m
  ```

  * Xms : 한 앱 실행하는데 최소 소요하는 크기(속도?)
  * Xmx : 한 앱 실행하는데 최대 소요하는 크기(속도?)

<br>

---

<br>

## STS

#### 인코딩 설정

* 다른 사람과 협업할 때 인코딩 에러를 안내기 위해 사전에 인코딩 설정 완료해줘야 함

* window - Preferences - `enc` 검색 - [General] - [Workspace] - Text file encoding - Other 선택 - `UTF-8` - Apply and Close
* [Web], [XML] 탭 아래에 있는 것 모두 다 `UTF-8`로 변경!!

<br>

#### 띄울 웹 브라우저 설정

* STS - Window - Web Browser - [Chrome]

#### `.java` & `.class`

* 소스코드파일(`.java`)와 컴파일된코드파일(`.class`)는 따로따로 관리가 됨
* 그래서 다른 폴더 안에 저장됨.
  * `.java` 는 src 폴더에
  * `.class` 는 bin 폴더에

<br>

#### Package

* C에서의 directory 개념

* 실무에서는 이름을 이렇게 관리...

  * `com.ssafy.team1.prj.어떤역할을하는`

  * 회사 싸피의 team1의 prj의 어떤 역할을 하는 패키지
  * `.` 들이 하위 디렉토리처럼 만들어짐!!!
  * 연관있는 것끼리 관리하기 위해서 이런식으로 만들어짐

<br>

#### 리팩토링

* `java class명`이나 `package명` 변경하고 싶을 때 리팩터를 통해 변경!!

<br>

#### 단축키

* 자동 완성 : `ctrl` + `space`
* 문단 이동 : `alt` + `↓`

<br>

#### Export

General - Archieve File 형식

<br>

#### Import

General - Existing Projects into Workspace 형식

<br>

---

<br>

## JAVA

#### 클래스

* 클래스 명의 첫번째 단어는 반드시 **대문자**로
* 클래스의 구성 요소
  * 데이터(변수) + 기능(메소드)

<br>

#### static

* **그냥 호출해도 호출되게 해줌**
  * 그래서 `main`에 static 사용함
  * `public static void main(String() args){}`

* 자동으로 메모리에 띄어주기 때문!
  * 따라서 사용할 때 타입 선언만 해줘도 사용 가능 
* static 지정 안한 것 사용하려면,,
  * 키워드 `new` 사용하여 메모리에 띄어줘야 함

<br>

#### 변수 캐스팅 (형변환)

* 기본으로 인식하는 것

  * 정수 : Integer
  * 실수 : Double

* 기본 말고 선언해야 할 때는 명시적으로 선언해야 함. 안하면 에러

  `float num = (float) 99.99;`

* 캐스팅

  * 큰 크기의 타입을 작은 크기의 타입으로 변경할 경우 명시적 타입 변환을 해줘야 함

* 변수 클래스

  * Integer, Long 등등
  * 사용 예시
    * `Integer.MAX_VALUE` 
    * integer형의 Max값이 반환됨

* 문자열 형변환

  * `parse`

  ```java
  int jumsu = Integer.parseInt("90");
  		double jumsu2 = Double.parseDouble("90.99");
  ```

<br>

#### 출력

```java
System.out.println(변수명)
System.out.printf("%변수타입", 변수명)
```

<br>

#### 입력

```java
Scanner scanner = new Scanner(System.in);
int n = scanner.nextInt()
```

<br>

#### 배열

* 기본 사용

  * 방법 1

  ```java
  int[] num; // 배열 선언
  num = new int[5]; // 배열 생성
  ```

  * 방법2

  ```java
  int[] num = new int[7];
  ```

  * String

  ```java
  String[] names = new String[] {"홍길동", "김길동", "박길동", "고길동", "이길동"};
  
  String[] names = {"홍길동", "김길동", "박길동", "고길동", "이길동"};		
  ```

  

* 배열 길이

  ```java
  num.length
  ```

* 배열 한 번에 출력

  ```java
  System.out.println(Arrays.toString(num))
  ```

  