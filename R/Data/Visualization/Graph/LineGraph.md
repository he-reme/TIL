# 선그래프

* 시간의 변화에 따라 수집된 데이터를 시각화하는 데 주로 사용됨
  * 예) 연도별 인구 증가 추이
* `x축`을 시간축으로 하여 선그래프를 그리면
  * 시간 변화에 따른 데이터의 증감 추이 쉽게 확인 가능
  * 시간 변화에 따라 데이터를 수집한 경우 : **시계열 데이터** 라고 함



---



## 선그래프 작성

#### 하나의 선그래프 그리기

```R
month <- 1:12                         # 1월 ~ 12월
late  = c(5,8,7,9,4,6,12,13,8,6,6,4)  # 월별 지각생 수
plot(month,                           # x data
     late,                            # y data
     main='지각생 통계',                # 제목 
     type='l',                        # 그래프의 종류 선택(알파벳) 
     lty=1,                           # 선의 종류(line type) 선택
     lwd=1,                           # 선의 굵기 선택
     xlab='Month',                    # x축 레이블
     ylab='Late cnt',                 # y축 레이블
     ylim = c(1:20)                   # y축 범위 설정 
)
```

* `type` : 그래프 종류
  * `l` 
    * 평범한 선
  * `b` 
    * 값에 점
    * 선과 점은 만나지 않음
  * `s`
    * 네모네모 선
    * 막대그래프같이 그려지지만, 겉면만 그려진다고 생각하면 됨
  * `o`
    * 값에 점
    * 선이 점을 지남
* `lty` : 선의 종류
  * `1`
    * 그냥 평범한 선
  * `2`
    * `---------------------`
    * 짧은 끊어진 선
  * `3`
    * `.....................`
    * 점 선
  * `4`
    * `_._._._._._._._._._._`
    * `2번 선` + `3번 선`
  * `5`
    * `ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ`
    * 조금 긴 끊어진 선
    * `2`번보다 길다
  * `6`
    * `ㅡ.ㅡ.ㅡ.ㅡ.ㅡ.ㅡ.ㅡ.ㅡ.ㅡ.`
    * `5번 선` + `3번 선`

#### 복수의 선 그래프 그리기

```R
month = 1:12
late1  = c(5,8,7,9,4,6,12,13,8,6,6,4)      # 학급1의 지각생 수
late2  = c(4,6,5,8,7,8,10,11,6,5,7,3)      # 학급2의 지각생 수

plot(month,                                # x 데이터
     late1,                                # y 데이터
     main='Late students',                 # 그래프 제목
     type='b',                             # 그래프의 종류 선택(알파벳)
     lty=1,                                # 선의 종류(line type) 선택
     col='red',                            # 선의 색깔 선택          
     xlab='Month',                         # x축 레이블
     ylab='Late cnt'                       # y축 레이블
)
lines(month,                               # x 데이터
      late2,                               # y 데이터
      type='b',                            # 선의 종류(line type) 선택
      col='blue')                          # 선의 색깔 선택
```

* `lines()` 
  * `plot()` 함수로 작성한 그래프 위에 선을 겹쳐서 그리는 역할
  * 이 함수를 추가할 때마다 선이 하나씩 추가됨



---



## 그래프 꾸미기

#### 축 바꾸기

```R
month <- 1:12                         # 1월 ~ 12월
late  = c(5,8,7,9,4,6,12,13,8,6,6,4)  # 월별 지각생 수
plot(month,                           # x data
     late,                            # y data
     main='지각생 통계',                # 제목 
     type='l',                        # 그래프의 종류 선택(알파벳) 
     lty=1,                           # 선의 종류(line type) 선택
     lwd=1,                           # 선의 굵기 선택
     xlab='Month',                    # x축 레이블
     ylab='Late cnt'                  # y축 레이블
     axes=F     # 축 눈금 다른거로 쓰고싶으면! 이걸 꼭 해줘야 함.
)
axis(1,at=1:12,lab=c("1월","2월","3월","4월","5월", ...)) # x축 눈금 바꾸기
axis(2, at=late)  # y축 방법1: 위와 동일
axis(2,ylim=c(0,20)) # y축 방법2: 원래 값으로 나오게 하고싶을 때 
```


