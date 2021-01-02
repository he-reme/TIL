# Git을 이용한 협업

> 협업 모델..

* Push & Pull
  * 단점 : 동시 작업 불가 (비동기적)
  * 비효율적.. -> 그래서 동시 작업을 위해 branch 가 있는 것
* Fork & Pull Request(PR)
* ~~Shared Repo with Branching & PR~~



## Git Branch

> **`branch`는 일회용이다.**
>
> `merge` 가 이뤄진 `branch` 는 휴지통으로~!



### `git branch`

* 현재 git에서 관리하고 있는` branch` 들을 출력
* 현재 `HEAD` 가 가리키고 있는 `branch` 를 표시



### `git branch [브랜치 이름]`

* 새로운 `branch` 를 만듬



### `git checkout [브랜치 이름]`

* `branch `를 이동

* (커밋 간 이동)



### `git merge [브랜치 이름]`

* `branch` 병합



### `git branch -d [브랜치 이름]`

* `branch` 삭제



---



## Pull Request 

### 웹 사이트(github)에서 merge하는 방법

* 팀원이 바로 `master branch`에 변경사항을 반영하면 문제가 발생하므로 사용하는 방법

* 과정

  * 팀원이 `master branch` 관리자에게 `pull request` 를 보냄
  * 관리자에게 허가 받으면 `merge`가 이루어짐

  

### 연습하기

#### `branch` 와 `pull request` 를 활용하여 강의 피드백 반영하기

1. 저장소(피드백 프로젝트)를 `clone` 받습니다.

2. 본인의 영어 이름의 `branch`를 생성 후 이동합니다.

   ex) 

   ```노디ㅣ
   $ git branch hereme
   $ git checkout hereme
   ```

   

3. 본인의 이름을 딴 마크다운 파일 `한글이름.md`을 생성 후, 이번 수업에 대한 질문, 기타 궁금한 사항, 피드백을 적습니다.