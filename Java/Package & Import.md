# Package & Import

<br>

---

<br>

## Package

* PC의 많은 파일 관리 → 폴더 이용
  * 유사한 목적의 파일을 기준으로 작성
* 프로그램의 많은 클래스 → 패키지 이용
  * 패키지는 클래스 파일을 담고 있는 디렉터리
  * 패키지 이름은 의미 있는 이름으로
  * `.`을 통해 계층적 접근
* package 선언
  * `package package_name;`
  * 주석, 공백을 제외한 첫 번째 문장에 하나의 패키지만 선언
  * 모든 클래스는 반드시 하나의 패키지에 속한다
    * 생략시 `default package`
    * 생략 안하는게 좋다!!!!
* 일반적인 package naming 룰
  * **`소속.프로젝트.용도`**
  * 예) `com.ssafy.hrm.common`
    * `com.ssafy` : 회사의 identity
    * `hrm` : project
    * `common` : 용도

<br>

---

<br>

## import

> 단축키 : `ctrl` + `shilft` + `O` 

* 다른 패키지에 선언된 클래스를 사용하기 위한 키워드
  * 패키지와 클래스 선언 사이에 위치
  * 패키지와 달리 여러 번 선언 가능
* 선언 방법
  * `import 패키지명.클래스명;`
  * `import 패키지명.*`
    * 하위 패키지까지 import 하지는 않음
* import한 package의 클래스 이름이 동일하며 명확히 구분해야할 때
  * 클래스 이름 앞에 전체 패키지 명을 입력
    * 예) `java.util.List list = new java.util.ArrayList();`
* default import package
  * `java.lang.*;`

<br>

---

<br>

## 일반적인 클래스 레이아웃

* 패키지 선언부
* 외부 패키지 import
* class 선언부
* 멤버 변수
* 초기화 블록
* 생성자
* 멤버 메서드

<br>

---

