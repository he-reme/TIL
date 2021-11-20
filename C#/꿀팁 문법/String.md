# String

<br>

#### 목차

* Replace
* Split

<br>

---

<br>

## Replace

> 문자열 내의 특정 문자열 변환

#### 문법

```c#
str.Replace("교체할 문자열", "대체할 문자열");
```

<br>

#### 예제

```c#
string str = "hello my name is hyerim";

str = str.Replace("h", "H");
```

* 결과 : `Hello my name is Hyerim`

<br>

---

<br>

## Split

> 특정 문자열 기준으로 자르기

#### 문법

```c#
str.Split("기준문자열");
```

<br>

#### 예제

```c#
string[] input = Console.ReadLine().Split();
```

* 생략시 **공백** 기준으로 잘라짐
