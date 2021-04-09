# AWS

> 상용화되어 있는 클라우드 서버

#### AWS에서 공부하면서 사용할 환경

* 유분투 리눅스 운영체제
  * 정해진 명령어를 사용해서 작업 수행
  * 리눅스 운영체제 : 다중 
  * 명령어 예시 : ls, cat, rm, cd, more

* mongodb
  * 반정형, 비정형 데이터 저장소
  * json 형식으로 데이터를 저장, 추출
  * pymongo 모듈 사용
* mariadb
  * 정형데이터 저장소
  * db테이블, SQL 언어 사용해서 데이터를 저장, 추출
  * pymysql 모듈 사용
* anaconda
  * jupyter lab

#### 서버 사양

* SW
  * RStudio
  * R
  * Anaconda3
  * python 3.7.6



---



#### putty

* AWS 서버(리눅스)
* 터미널(명령처리), 서버 접속
* telnet : 클라이언트에서 연결을 끊을 때까지 연결 상태를 유지

#### FileZilla

* AWS 서버(리눅스)
* 원격 서버로 파일 전송
* ftp : 일정 시간동안 사용하지 않으면 자동으로 서버와의 연결 종료
* 왼쪽창 : 내 컴퓨터
* 오른쪽창 : 원격 서버

#### 주피터 랩

* 데이터 분석
* 기동 시키기
  * putty 실행
  * 원하는 폴더에서 해당 명령어 수행
    * `jupyter lab --ip=0.0.0.0 --no-browser --port=8907`
    * 맨 마지막 URL 복사 후 Chrome에서 열기~!