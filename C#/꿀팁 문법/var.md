# var

> auto 변수

* 모든 변수 생성에 사용 가능하다...
  * 배열 : `var array = Console.ReadLine().Split();`
  * 딕셔너리 : `var dict = new Dictionary<string,int>();`

<br>

---

<br>

#### 사용에 대한 제약 조건

* 지역 변수에만 사용 가능
* 변수 선언과 동시에 반드시 초기화 되어야 함
* null, 메소드 그룹, 익명 함수로 초기화 불가

<br>

#### 사용되는 경우

* 특정 타입의 이름이 길어서 입력하기 번거로운 경우
* 타입이 명확한 경우
* 코드의 가독성을 높이기 위한 경우

<br>

#### 반드시 사용해야 하는 경우

* LINQ 쿼리식에서 무명 타입의 속성(Uppder/Lowwer)에 접근하기 위해 반드시 var 키워드로 변수를 선언해야 함 

<br>

---

<br>

#### foreach와 같이 사용

```
// input
1 2 3 4 5
```

```c#
var input = Console.ReadLine().Split();

foreach (var n in input)
{
	// ...
}
```

