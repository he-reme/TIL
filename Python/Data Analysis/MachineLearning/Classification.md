# 분류 알고리즘

* 예측하려는 대상의 속성(설명변수)를 입력 받고, 목표 변수가 갖고 있는 카테고리(범주형) 값 중에서 어느 한 값으로 분류하여 예측함

* 고객 분류, 질병 진단, 스팸 메일 필터링, 음성 인식 등 목표 변수가 카테고리 값을 갖는 경우에 사용

#### 종류

* KNN
* SVM
* Decision Tree
* Logistic Regresstion
* 등



---



## KNN

> k - Nearest - Neighbors
>
> k개의 가까운 이웃이라는 뜻

#### 원리

* 새로운 관측값이 주어지면 기존 데이터 중에서 가장 속성이 비슷한 k개의 이웃을 먼저 찾는다.
* 그리고 가까운 이웃들이 갖고 있는 목표 값과 같은 값으로 분류하여 예측한다.

* **k값에 따라 예측의 정확도가 달라짐**
  * 적절한 K값을 찾는 것이 매우 중요!!

#### 과정

1. 데이터 준비

2. 데이터 탐색

3. 속성 선택

   * 변수로 사용할 후보 열 선택
     * 예측 변수를 나타내는 열 추가하고,
     * 설명변수로 사용할 후보 열 포함시키기

   * 범주형 데이터를 숫자형으로 변환
     * 원핫 인코딩 ( = 더미변수를 만드는 과정)
     * `concat()` 함수를 사용해서 기존 데이터프레임에 생성된 더미 변수 열을 연결하고, 기존의 범주형 데이터열들은 삭제

4. 훈련/검증 데이터 분할

   * 변수 X, y 할당

     ```python
     X = df[['설명변수열리스트']]
     y = df['예측변수열']
     ```

     * 예측 변수 열을 변수 y에 저장하고,
     * 나머지 열들을 설명 변수로 사용하기 위해 변수 X에 할당

   * 설명 변수 열들이 갖는 데이터의 상대적 크기 차이를 없애기 위해 **정규화** 과정 거치기

     * sklearn의 preprocessing 모듈 사용

       ```python
       from sklearn import preprocessing
       X = preprocessing.스케일러명().fit(X).transform(X)
       ```

       * MinMaxScaler
       * MaxAbsScaler
       * StandardScaler
       * RobustScaler

   * 훈련 데이터와 검증 데이터를 나눔

     * skearn의 `train_test_split()` 메소드 사용

       ```python
       # 훈련, 검증 데이터를 7:3 비율로 구분
       from sklearn.model_selection import train_test_split
       X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=10)
       ```

5. 모형 학습 및 검증

   * 모형 학습
     * **sklearn** 라이브러리의 **neighbbors 모듈** 사용
   * 모형의 예측 능력 평가
     * Confusion Matrix 계산
     * 평가 지표 계산

#### 모형 학습

1. **sklearn** 라이브러리의 **neighbbors 모듈** 사용

2. `KNeighborsClassifier()` 함수로 KNN 분류 모형 객체를 생성하여 변수 knn에 저장

   * `n_neighbors` 옵션 : 이웃 숫자 k

3. 훈련 데이터 (`X_train`, `y_train`)를 `fit()` 메소드에 입력하여 모형을 학습시킴

4. 검증 데이터 (`X_test`)를 `predict()` 메소드에 전달하여, 모형이 분류한 예측값을 변수 `y_hat`에 저장

5. 이 값을 실제 값이 들어 있는 y_test와 비교!

   ```python
   # sklearn 라이브러리에서 KNN 분류 모형 가져오기
   from sklearn.neighbors import KNeighborsClassifier
   
   # 모형 객체 생성 (k=5로 설정)
   knn = KNeighborsClassifier(n_neighbors=5)
   
   # train data를 가지고 모형 학습
   knn.fit(X_train, y_train)
   
   # test data를 가지고 예측(분류)하고 예측값을 y_hat에 저장
   y_hat = knn.predict(x_test)
   
   # 시각적으로 확인해보기
   print(y_hat[0:10])
   print(y_test.values[0:10])
   ```

#### 모형 검증

* 모형의 예측 능력을 평가

  * metrics 모듈의 `confusion_matrix()` 함수를 사용하여 Confusion Matrix를 계산

    ```python
    # 모형 성능 평가 - Confusion Matrix 계산
    from sklearn import metrics
    knn_matrix = metrics.confusion_matrix(y_test, y_hat)
    print(knn_matrix)
    ```

  * 예시 실행 결과

    ```
    [[109  16]
     [ 25  65]]
    ```
    * test data 개수(215) 중
      * TP (0으로 정확히 예측한 개수) : 109
      * FP (0을 1로 잘못 분류한 개수) : 16
      * NP (1을 0으로 잘못 분류한 개수) : 25
      * TN  (1로 정확히 예측한 개수)

* 모형의 예측 능력을 평가하는 지표 계산

  * metrics 모듈의 `classification_report()` 함수 사용

    ```python
    # 모형 성능 평가 - 평가 지표 계산
    knn_report = metrics.classification_report(y_test, y_hat)
    print(knn_report)
    ```

    * 출력하는 지표
      * precision
      * recall
      * f1-score
      * support

#### 분류 모형의 예측력을 평가하는 지표

* Confusion Matrix

  * 모형이 예측하는 값에 두 가지가 있을 때
    * True / False (로 그냥 나타냄)
    * 각 예측값은 실제로 True / False 일 수 있다.

  * 실제값을 x축으로, 예측값을 y축으로 하는 2X2 매트릭스로 표현한 것

  ```
  	T			TP					FP
  예		(True Positive)		(False Positive)
  측
  값
  	F			FN					TN
  		(False Negative)	 (True Negative)
  	
  				T					 F
  						실제값
  ```

  ```
  # 실제 출력
  [[109  16]
   [ 25  65]]
  ```

* 정확도 (Precision)

  * True로 예측한 분석대상 중에서 실제 값이 True인 비율
  * 모형의 정확성을 나타내는 지표가 됨
  * 정확도가 높다는 것
    * FP (False Positive, 실제 False를 True로 잘못 예측) 오류가 작다는 뜻
  * `Precision = TP / (TP + FP)`

* 재현율 (Recall)

  * 실제 값이 True인 분석대상 중에서 True로 예측하여 모형이 적중한 비율
  * 모형의 완전성을 나타내는 지표
  * 재현율이 높다는 것
    * FN (False Negative, 실제 True를 False로 잘못 예측) 오류가 낮다는 뜻
  * `Recall = TP /  (TP + FN)`

* F1 지표 (F1-score)

  * 정확도와 재현율이 균등하게 반영될 수 있도록 정확도와 재현율의 조화 평균을 계산한 값
  * 모형의 예측력을 종합적으로 평가하는 지표
  * 값이 높을수록 분류 모형의 예측력이 좋다고 말할 수 있음

  * `F1-score = 2 * (Precision * Recall) / (Precision + Recall)`