# String

#### 문자열 합치기

* 문자열을 단순히 `+`를 사용해서 합치면 메모리를 효율적으로 사용하는 방법이 아니므로 지양!!!

* 방법1

  ```java
  int x = 22;
  String str = "hi"
  String info = String.format("이것이 문자열 합치기다 %d %s", x, str); 
  		
  ```

* 방법2

  ```java
  StringBuilder sb = new StringBuilder();
  int x = 22;
  sb.append("문자열");
  sb.append(x);
  return sb.toString(); // "문자열22"
  ```

  