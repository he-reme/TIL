# 아나콘다

* Anaconda라는 곳에서 만든 파이썬 배포판
* 수백 개의 파이썬 패키지를 포함함
* 회사 내에서도 상업용으로 무료로 사용할 수 있다는 장점이 있음

* 설치

  `https://www.anaconda.com/products/individual`



---



## Jupyter Lab

> Jupyter Notebook과 비슷한 개발 환경
>
> 브라우저를 통해서 개발 페이지를 제공함

* Jupyter Notebook은 파일 목록이 안보이지만
* Jupyter Lab은 볼 수 있어서 더 편리하다.

#### Jupyter Lab 열기

1. `Anaconda Prompt` 창 열기
2. `jupyter lab` 명령 입력
   * 브라우저로 `JupyterLab` 열기

#### Jupyter Lab 강제 종료

`ctrl` + `c`

#### 환경 설정

> 자동으로 인식하게 되는 현재 디렉토리 위치는 시스템 사용자명 디렉토리이기 때문에 ,
>
> 원하는 디렉토리로 변경해주기 위해서는 해당 환경설정을 해줘야 함

1. `Anaconda Prompt` 창 열기
2. `jupyter notebook --generate-config` 명령 실행
   
* 설정 파일 생성
  
3. `C:\Users\H\.jupyter` 경로를 찾아간다.

   * 컴퓨터에 따라 사용자이름(`H`)은 다름

4. `jupyter_notebook_config.py` 파일을 메모장으로 오픈

5. `c:/KHR/` 경로에 `PYDATAexam` 폴더 생성

6. `373`행으로 이동 후 다음과 같이 수정

   * 디렉토리 위치 변경

   ```R
   ## The directory to use for notebooks and kernels
   # Default:"
   c.NotebookApp.notebook_dir = 'c:/KHR/PYDATAexam'
   ```

7. `Anaconda Prompt` 창 열고, `jupyter lab` 명령 실행
   
   * `serving notebooks from local directory`(디렉토리 위치)가 변경된 것을 확인할 수 있음



---



## Anaconda에 가상환경 만들기

> 가상환경 만드는 이유? 
>
> 1. python 버전 관리와 패키지 충돌 방지
> 2. 해당 프로젝트에서 필요한 패키지만 설치하기 위해
>
> 따라서 프로젝트별로 각각의 가상환경을 만들고 해당 환경에서 개발하는 것이 바람직함.

* `pydatavenv` 라는 커널 생성하기

* 해당 이름은 내가 원하는 이름으로 만든거임!

1. 파이썬 3.8 기반의 가상환경 `pydatavenv`를 생성하는 명령 실행

   ```sh
   conda create --name pydatavenv python=3.8
   ```

   * 실행중 `Proceed ([y]/n)?` 이 뜨면 `y` 입력

2. 가상 경이 잘 만들어졌는지 확인

   ```shell
   conda info --envs
   ```

   * 이렇게 뜨면 성공

     ```shell
     # conda environments:
     #
     base                  *  C:\Users\H\anaconda3
     pydatavenv               C:\Users\H\anaconda3\envs\pydatavenv
     ```

3. 가상환경 활성화

   ```shell
   conda activate pydatavenv
   ```

4. `ipykerner` 설치

   ```shell
   conda install ipykernel
   ```

   * 실행중 `Proceed ([y]/n)?` 이 뜨면 `y` 입력

5. `pyzmq` 삭제 후 재설치

   ```shell
   pip uninstall pyzmq
   pip install pyzmq
   ```

6. `pydatavenv` 라는 가상환경을 `jupyter lab`의 커널로 등록

   ```shell
   python -m ipykernel install --user --name pydatavenv
   ```

   * 커널 : 실행환경

7. `Anaconda Prompt` 창 한 개 더 오픈
8. `jupyter lab` 명령 실행

#### `pydatavenv` 가상환경에 추가 패키지 설치하기

* `pydatavenv` 가상환경 활성화된  `Anaconda Prompt` 창에서 아래 명령들 하나씩 입력

  * 가상환경 활성화 : `conda activate pydatavenv`
  
* 크롤링을 위한 패키지

  ```shell
  conda install requests
  conda install pillow
  conda install bs4 # beautiful soup. 파이썬 정적 크롤링
  conda install selenium # 파이썬 동적 크롤링
  conda install lxml
  conda install html5lib
  pip install tweepy
  ```

* 시각화를 위한 패키지

  ```shell
  conda install pandas
  conda install matplotlib
  conda install seaborn
  pip install folium
  conda install scikit-learn
  conda install xlrd
  conda install -c conda-forge googlemaps
  conda install openpyxl
  ```

  * 패키지 설치 잘 안될 때, `pyzmq` 삭제 후 재설치 

    ```
    pip uninstall pyzmq
    pip install pyzmq
    ```

* opencv 설치 패키지

  ```
  conda install opencv
  pip install opencv-python
  conda install missingno
  pip install statsmodels
  ```

* 텍스트분석을 위한 패키지

  ```
  pip install konlpy
  pip install wordcloud
  pip install nltk
  pip install hgtk
  pip install netsorkx
  pip install apriori apyori
  pip install mlxtend
  pip install git+https://github.com/haven-jeon/PyKoSpacing.git
  pip install git+https://github.com/ssut/py-hanspell.git
  ```

  * jpype 설치

    * `https://www.lfd.uci.edu/~gohlke/pythonlibs/#jpype`

    * `C:\Users\H` 디렉터리에 넣고 확인

      ```
      dir *.whl
      ```

    * 확인한 이름으로 다운로드

      ```
      pip install JPype~~~
      ```

      

* `conda list` 로 설치한 패키지 확인 가능
* 설치가 완료됐으면 `pydatavenv` 비활성화

  * 가상환경 비활성화 : `conda deactivate`

#### 동적 크롤링을 위한 환경설정

> 크롬 드라이브 다운로드

1. 크롬이 최신 버전인지 먼저 확인

2. `https://sites.google.com/a/chromium.org/chromedriver/` 이동
3. Downloads - Latest stable release - `ChromeDriver89.0.4389.23` 선택
4. `chromedriver_win32.zip` 설치
5. 압축 해제 후 `chromedriver.exe` 파일을 `c:\Temp` 디렉토리에 저장



---



