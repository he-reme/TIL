# JSON

> JavaScript Object Notation
>
> 인터넷에서 자료를 주고 받을 때 그 자료를 표현하는 방법

* 자료의 종류에 큰 제한은 없으며, 특히 변수값을 표현하는 데 적합
* 형식은 자바스크립트의 구문을 따르지만, 프로그래밍 언어나 플랫폼에 독립적
  * C, C++, C#, 자바, 자바스크립트, 펄, 파이썬 등 많은 언어에서 이용 가능
  * javascript문서와 가장 잘 맞음

#### 목차

* JSON 문법
* JSON 장점
* XML
* JSON과 XML 비교



---



## JSON 문법

#### 인코딩

* 유니코드

#### 기본 자료형

* 숫자, 문자열, 참/거짓, null

#### 집합 자료형

* 배열, 객체



---



## JSON 장점

* 텍스트로 이루어져, 사람과 기계 모두 일고 쓰기 쉬움
* 프로그래밍 언어와 플랫폼에 독립적이므로, 서로 다른 시스템간에 객체를 교환하기 좋음
* 개방형 표준이며, 읽기 및 쓰기가 쉽고 가벼움



---



## XML 

> Extensible Markup Language
>
> 규격화 시킨 문서를 만들고 싶을 때 사용
>
> 태그명을 용도에 맞게 직접 정의하여 사용 가능

* HTML 
  * 페이지 제작에 사용되는 전용 마크업언어



---



## JSON과 XML비교

#### JSON 형식

```json
{
	"students":{
		"student":[
			{"name":"김혜림", "gender":"여"},
			{"name":"김정섭", "gender":"남"},
		]
	}
}
```

#### XML 형식

```xml
<students>
	<student>
		<name>김혜림</name> <gender>여</gender>
	</student>
	<student>
		<name>김정섭</name> <gender>남</gender>
	</student>
</students>
```



---

