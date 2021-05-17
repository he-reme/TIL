# TabView

## 구성

* Activity
  * TabLayout과 ViewPager 연결
  * ViewPager의 페이지가 변경될 때 알려주는 리스너 구현
  * Tab이 선택되었을 때 알려주는 리스너 구현
* Adapter
* Fragment
  * 실제 탭



---

## Fragment로 데이터 전달

> * Bundle 이용
>
> * 액티비티 > Fragment
>
> * Fragment > Fragment

#### `Intent` vs `Bundle`

* Intent 
  * 애플리케이션 내 **액티비티** 간의 데이터를 전달할 때 사용하는 클래스
* Bundle
  * 문자열로 된 키와 여러가지 타입의 값을 매핑하여 저장하는 Map 클래스
  * 다양한 데이터 타입 전송 가능
  * Fragment에서 사용

#### 1. 데이터를 전송하는 쪽

* `setArgment()`

  ```
  Fragment1 fragment1 = new Fragment1(); # fragment 생성
  
  //프레그먼트끼리 Name넘기기 위한 bundle
  Bundle bundle = new Bundle();
  bundle.putString("Name", name);
  fragment1.setArguments(bundle); //Name 변수 값 전달. 생략시 받는 쪽에서 null 값으로 받음
  ```
  
  * `Fragment1` 은 데이터를 전송할 Fragment 클래스명

#### 2. 데이터를 받는 쪽

* `getArgment()`

  ```
  // 번들 받기. getArguments() 메소드로 받음.
  Bundle bundle = getArguments();
  
  if(bundle != null){
      String name = bundle.getString("Name"); //Name 받기.
      System.out.println(name); //확인
  }
  ```

  * onCreateView??????? 더 채워넣어야 할듯?????