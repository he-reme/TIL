# Git

* 코드 관리 도구 (add, commit)
* 코드 저장 도구 (remote, push)
* **협업** 도구 (branch)
* 기본적 명령 사용 법 : `git ~~`



## SCM & VCS

* SCM (Source Code Management) : (소스)코드 관리 도구
* VCS (Version Control System) : 버전(형상) 관리

> 즉, Git은 버전을 통해 코드 관리 도구



---



## Git 기본 명령어

### `git init` 

* `git` 으로 코드 관리를 시작 (initate)
* *(**중요**) git은 폴더를 기준으로 프로젝트(코드) 관리*
  1. `.git` 폴더 생성
  2. git으로 프로젝트 관리 시작
  3. `(master)` 프롬프터가 생성됨
* 해당 프로젝트를 깃으로 관리하기 싫으면 `./git` 폴더 삭제해주면 됨



## `git status`

`git` 의 상태를 출력

강사님이 개인적으로 중요하다고 생각하시는 명령어. 

* 생성 직후

```shell
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

* `a.txt` 파일 생성 후

```
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        a.txt

nothing added to commit but untracked files present (use "git add" to track)
```

> commit (=save)

* `git add a.txt` 명령어 수행 후

```
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   a.txt
```



### `git add [파일/폴더명]`

저장을 위한 준비

* `git restore --staged [파일명]` : 특정 파일 add 취소하기



### `git commit -m '커밋메시지'`

준비된 파일/폴더의 버전을 생성(현재 상태 스냅샷, 현재 상태 저장)

* 버전 : 날짜, 누가 기록, **커밋(버전) 메시지**, 커밋 해쉬(hash) 등을 담음



### git 환경설정

* `git config --global user.email` '깃허브에 등록한 내 이메일'
* `git config --global user.name '등록할 이름'`



### `git log`

현재까지의 버전 히스토리 출력

버전 리스트 확인 가능

* `git log --oneline`



### `git checkout`

* `git log --oneline` 을 통해 구한 해시 아이디를 이용해 해당 버전으로 이동함. 
* 최신 버전들이 삭제된 것은 아님.
* `git checkout master` 로 하면 다시 가장 최신 버전으로 돌아옴..

### 	

### `git diff [파일명]`

이전 버전과의 차이를 출력



---



### `git remote`

원격 저장소의 정보를 출력

* `git remote -v` : 상세한 원격 저장소 정보 출력 (verbose)



### `git remote add [원격 저장소 이름] [원격 저장소 주소]`

* 일반적으로 첫번째 원격 저장소의 이름은 origin (원본) 으로 설정함.
* 그래서,, `git remote add origin [주소]` 라 설정 많이 함.
* 원격 저장소 주소 : github 원격 저장소 생성 후 받는 URL



### `git push [원격 저장소 이름] [브랜치 이름]`

> 차이를 올릴 때
>
> 반대는 `pull`

* 일반적으로 첫번째 원격 저장소의 이름은 `origin` (원본)

* 일반적으로 기본 브랜치의 이름은 `master`

* `git push origin master`

  

---



### `git clone [원격 저장소 주소]`

> `git clone [원격 저장소 주소] [원하는 폴더명]` 로도 사용 가능

* 처음 프로젝트를 복제해올 때 (시작할 때 1번만 쓰는 명령어)
* 통쨰로 들고오는 것
* `init` 과 비슷한 개념
* `git remote add` 과정도 포함됨



### `git pull [원격 저장소 이름] [브랜치 이름]`

> 차이를 가져올 때
>
> 반대는 `push`

* 일반적으로 첫번째 원격 저장소의 이름은 `origin` (원본)
* 일반적으로 기본 브랜치의 이름은 `master`
* `git pull origin master`



---



## 추가적인 명령어



### `code .`

코드 에디터 실행 명령어

