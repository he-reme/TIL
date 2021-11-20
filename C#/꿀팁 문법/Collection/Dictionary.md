# Dictionary

> Key-Value 쌍 형식으로 데이터 저장

```c#
using System.Collections.Generic;
```

<br>

---

<br>

## 기본 구조

```c#
Dictionary<Tkey, Tvalue> dict = new Dictionary<Tkey, Tvalue>();
```

<br>

#### 데이터 삽입

* 방법1

  ````c#
  dict.Add(key, value);
  ````

  * **이미 있는 key를 Add 하려고 하는 경우 런타임 에러 발생**
  * `Add` 메소드를 이용하여 데이터를 삽입할 때는 꼭 이미 존재하는지 확인 후 사용 
    * `ContainsKey` 메소드와 같이 사용

* 방법2

  ```c#
  dict[key] = value;
  ```

  * 이미 있는 key인 경우에도 런타임 에러 발생시키지 않음
  * 단, 없는 key인 경우 `dict[key]++`와 같이는 사용 불가

<br>

#### 데이터 획득 방법

* 방법1

  ```c#
  Tvalue value = dict[key];
  ```
  * 해당 key가 존재하지 않으면 error 발생

* 방법2 ★

  ```c#
  Tvalue value = null;
  dict.TryGetValue(key, out value);
  ```
  * 해당 key가 존재하지 않아도 error 발생하지 않음 

  * `TryGetValue` 메소드는 기본적으로 해당 dictionary에서 입력받은 키를 찾아서 해당 키가 존재하는지 여부를 bool 타입으로 리턴함

  * 원하는 키에 대한 유효성 체크만 원하는 경우 유용

    ```c#
    // value 값을 사용하고 싶을 경우
    if(dict.TryGetValue(key, out int value))
    {
        // ...
    }
    ```

    ```c#
    // value 값을 사용하지 않고 유효성만 확인하는 경우
    if(dict.TryGetValue(key, out _))
    {
        // ...
    }
    ```

<br>

#### 원하는 키에 대한 유효성 체크

```c#
if(dict.ContainsKey(key))
{
	// ...
}
```



<br>

#### 예제

```c#
Dictionary<int, string> person = new Dictionary<int, string>();
person.Add(2, "hyerim");
person.Add(1, "gildong");

foreach(var pair in person)
{
	Console.WriteLine(pair);
}
```

* 출력

  ```
  [2, hyerim]
  [1, gildong]
  ```



<br>

---

<br>

## 순서가 있는 구조

> 데이터 쌍의 순서가 중요한 경우 사용

```C#
SortedDictionary<TKey, Tvalue> = new SortedDictionary<Tkey, Tvalue>();
```

* 디폴트
  * 키값을 기준으로 정렬

<br>

#### 사용

* 데이터 삽입
  * `Add(key, value)`



#### 예제

```C#
SortedDictionary<int, string> person = new SortedDictionary<int, string>();
person.Add(2, "hyerim");
person.Add(1, "gildong");

foreach(var pair in person)
{
	Console.WriteLine(pair);
}
```

* 출력

  ```c#
  [1, gildong]
  [2, hyerim]
  ```

  

