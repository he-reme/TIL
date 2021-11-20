# HeidSQL

> 이전에는 MySQL Front로 알려졌던 제품
>
> MySQL, MariaDB, SQLite 등의 **DBMS를 직접 접속하여 사용하려는 경우**에 선택할 수 있는 **DBMS 클라이언트** 무료 프로그램

 

---



## 이것저것

RDBMS에서 테이블 생성시 컬럼단위로 컬럼명과 타입을 설정

CharField -> VARCHAR



---



## 환경 설정

1. 신규 버튼 클릭
   * 신규 세션 생성
2. 네트워크 유형
   * SQLite (Experimental) 선택
3. 데이터베이스 파일명
   * 장고 프로젝트의 `db.sqlite3` 선택
4. SQLite로 세션 이름 변경
5. 오픈된 장고 프로젝트의 `db.sqlite3`에 `db` 라는 이름의 데이터베이스가 생성됨
6. `db`라는 이름의 데이터베이스에는 `python manage.py migrate` 명령의 실행에 의해서 생성된 테이블들이 여러개 존재
   *  그 중 모델 클래스에 의해 생성된 테이블도 확인 가능
7. 테이블 선택하면 여러가지 기능(데이터 확인, 쿼리문 작성 등) 이용 가능



---



## CSV 파일 데이터베이스로 만들기

* 만약 `excel` 스프레드시트일 경우
  *  저장할 때 형식을 csv로 지정할 수 있다

1. HeidSQL에서 해당 CSV 파일 내용에 맞는 테이블을 생성, 저장
   * `SQLite` > `db` > 새로 생성 > 테이블
   * 이름은 `앱이름_모델클래스명`

2. 도구 > CSV 파일 가져오기
   * 구분자 지정 (CSV 파일 메모장으로 열면 구분자 확인 가능)
   * 인코딩 UTF-8로 설정해야 한글 깨지지 않음

3. 파이참으로 이동

4. models.py에 테이블명과 동일한 모델 클래스 만들기

   * 대소문자 구분 없음

5. 생성한 모델 클래스에 import 하기

   * 쉘 실행 후 명령어 입력

   ```
   python manage.py shell
   >>> from thirdapp.models import Emp
   ```

5. 잘 진행 됐는지 확인하는 명령어

   ```
   >>> Emp.objects.all()
   ```

   

