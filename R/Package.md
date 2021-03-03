# R 패키지

* 여러 함수들을 묶어 놓은 것을 패키지
* R은 패키지 단위로 관리함
* 패키지 설치를 통해서 필요한 함수들을 확장하여 사용 가능
* R의 패키지들은 CRAN 사이트에서 다운로드하여 설치 가능



---



## API

> Application Programming Interface

* 자주 사용될 수 있는 기능들을 미리 만들어놓은 프로그램

* 어떠한 언어의 API 인가에 따라서 함수, 클래스 ...
  * R의 경우엔 대부분 함수



---



#### 새로운 R 패키지 설치

`install.packages("패키지명")`



#### 이미 설치된 R 패키지 확인

`installed.packages()`



#### 설치된 패키지 삭제

`remove.pachages("패키지명")`

-

#### 설치된 패키지의 버전 확인

`packagVersion("패키지명")`



#### 설치된 패키지 업데이트

`update.packages("패키지명")`



#### 설치된 패키지 로드

`library("패키지명")`

* 로드 실패시 ERROR

`require("패키지명")`

* 리턴값이 있음
  * 로드 성공 여부에 따라 TRUE, FALSE



#### 로드된 패키지 언로드 (로드 상태 해제)

`detach("package:패키지명")`



#### 로드된 패키지 검색

`search()`