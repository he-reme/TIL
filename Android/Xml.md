# Xml

> 앱에 보여지는 화면

#### 목차

1. 레이아웃
2. textView

---



## 1. 레이아웃

#### 에뮬레이터에 잘리지 않고 출력하기

* 최상위 레이아웃
  * height을 `match_parent` 로 설정
* 최상위 레이아웃의 하위 레이아웃
  * layout_weight로 배치하기
  * padding이나 margin값으로 조절하면 잘릴 수 있음..



---



## 2. textView

#### 가운데 정렬

```
android:textAlignment="center"
android:gravity="center"
```

* 위아래 정렬 : `android:gravity="center"`
* 좌우 정렬 : `android:textAlignment="center"`

