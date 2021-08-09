# Java 기초

#### 중요 개념

* jre, jvm

* 가비지 컬렉터

<br>

#### 클래스 구성 요소

* 데이터 (변수)
* 기능 (메소드)

<br>

#### docs 확인하기

* 커서 대고
* `ctrl` + 마우스 우클릭

<br>

#### 주석 단축키

* `ctrl` + `/`

<br>

#### `jar` 파일 추가하기

* 폴더 [eclipse] - [plugins]에 추가!

---

<br>

## cmd 창에서 컴파일, 실행

#### 컴파일

`javac -d . hello.java`

#### 실행

`java hello`

<br>

---

<br>

## 기본형

* int
* double

#### 연산

* `int`
  * 피 연산자의 크기가 4byte 미만이면 `int`로 변경한 후 연산 진행
  * `byte`끼리 연산해도 `int`로 변경 후 연산됨.
* 큰 타입
  * 두 개의 피연산자 중 큰 타입으로 형 변환 후 연산 진행
  * ex ) `long` + `int` → `long` + `long`

<br>

---

<br>

## 입출력

#### 입력

```java
import java.util.Scanner;

Scanner sc = new Scanner(System.in);

String s = sc.next();
int i = sc.nextInt();
double d = sc.nextDouble();
char c = sc.next().charAt(0);

sc.close();
sc = null;
```

* 변수 타입에 따라 `sc.nextXXX();`

* 파일을 읽어들여서 입력 받고 싶으면?

  ```java
  import java.io.FileInputStream;
  import java.util.Scanner;
  
  public static void main(String[] args) throws Exception{
  		System.setIn(new FileInputStream("input/input.txt"));
  		Scanner sc = new Scanner(System.in);
  		int T = sc.nextInt();
   		...   
  }
  ```

  * `throws Exeption` 추가

#### 출력

````java
System.out.printf();
System.out.println();
System.out.print();
````

* 자동 완성 : sysout + ctrl + space

<br>

---

<br>

## 영역

#### Heap

* 실제 객체를 저장
* `Reference Type`은 미리 만들 수 없는 데이터를 별도의 공간(heap)에 표현하고 그 공간의 주소를 저장함.

<br>

---

<br>

## 데이터 타입

* 기본 데이터 타입
  * 8가지
  * byte, short, int, long, float, double, boolean, char
* 참조형
  * 8가지의 나머지 모든 데이터 타입
  * String, int[], 사용자 정의 타입

<br>

#### 형변환

* 변수의 타입을 다른 타입으로 변환하는 것
* primitive는 primitive끼리, reference는 reference끼리 형 변환 가능
  * boolean은 다른 기본 타입과 호환되지 않음
* 명시적 형변환
  * 값 손실이 발생할 수 있으므로 프로그래머 책임하에 형변환 진행
* 묵시적 형변환
  * 자료의 손실 걱정 없으므로 JVM이 서비스 해줌.
* 방법
  * `int result = (int)d;`





<br>

---

<br>

## 비트

#### 비트 논리 연산자

* `&`
  * 두 피 연산자의 비트 값이 둘다 1이면 1, 나머지 경우 0
* `|`
  * 두 피 연산자의 비트 값이 하나라도 1이면 1, 둘다 0이면 0
* `^`
  * 두 피 연산자의 비트 값이 서로 다르면 1, 같으면 0
* `~`
  * 1이면 0, 0이면 1

<br>

#### 비트 이동 연산자 (쉬프트 연산자)

* `변수 << 숫자`
  * 숫자 만큼 왼쪽으로 이동, 빈 공간은 0으로 채움
* `변수 >> 숫자`
  * 숫자 만큼 오른쪽으로 이동, 빈 공간은 음수는 1, 양수는 0으로 채움
* `변수 >>> 숫자`
  * 부호 무시하고 숫자만큼 오른쪽으로 이동, 빈 공간은 0으로 채움

<br>

---

<br>

## 논리 연산자

* `&&`
  * `&`와 다르게 앞에서 `false`가 나오면 뒤의 논리 계산은 생략하고 바로 `false` 반환
* `||`
  * `&`와 다르게 앞에서 `true`가 나오면 뒤의 논리 계산은 생략하고 바로 `true` 반환

<br>

---

<br>

## Random 수 구현

#### `Math.random()`

* `Math.random()`
  * 0.0 <= x < 1.0
* `Math.random() * N`
  * 0.0 <= x < N.0
* `(int) (Math.random() * N)`
  * 0 <= x <= N-1
* `(int) (Math.random() * N) + 1`
  * 1 <= x <= N

#### `Random`

````java
import java.util.Random;
Random rand = new Random();
````

* `rand.nextInt(N)`
  * 0 <= x < N
* `rand.nextInt(N) + 1`
  * 1 <= x <= N

#### `%Operator`

* 충분히 큰 Random 수 % N
  * 0 <= x <= N-1
* 충분히 큰 Random 수 % N + 1
  * 1 <= x <= N

<br>

---

<br>

## 조건문

#### `if(----)`

* 논리형
  * boolean
* 비교식
  * x>=y
* Method call
  * isEven() 등등

#### `switch(----)`

* 정수
  * byte, short, char, int
* Enum
  * Day.MONDAY
* Class Object
  * Byte, Short, Character, Integer, **String**
* Method Call
  * getNumber 등등

<br>

---

<br>

## Break, Continue

#### 빠져 나올 반복문 지정 가능

```java
outer : for(int i=0; i<N; i++){
	for(int j=0; j<M; j++){
		if(j==100)
			break outer; // outer로 지정된 반복문으로 탈출
		if(j==10)
			continue outer; // outer로 지정된 반복문으로 continue
	}
}
```

* `break outer;`
  * outer로 지정된 반복문으로 탈출
* `continue outer;`
  * outer로 지정된 반복문으로 continue

<br>

---

<br>

## java.util.Scanner

#### 주요 API

* `.hasNext()`
* `.next()`
  * white space를 경계로 문자열 읽기
  * white space가 나오면 중지
* `.hasNextXXX()`
* `.nextXXX()`
  * Int, Float, Double ...
* `.nextLine()`
  * 개행 문자까지 읽기
  * 주의
    * 앞쪽에서 `nextInt()`로 입력 받았다면, 
    * `sc.nextLine()` 한번 써주고 이를 써줘야 원하는 입력을 받을 수 있음.
    * 개행문자가 읽히기 때문 
* `.next().charAt(0)`

<br>

---

<br>

#### 최대/최소

```java
int min = Integer.MAX_VALUE;
int max = Integer.MIN_VALUE;
```

```java
for (int num : arr) {
	min = Math.min(min, num);
	max = Math.max(max, num);
}
```

<br>

---

<br>

## 메모리 공간

#### stack

* 변수 (데이터의 주소를 가짐)

#### Heap

* 실질적인 데이터, new로 생성된 데이터
* 배열

