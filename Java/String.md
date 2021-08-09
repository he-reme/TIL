# String

* 불변의 성질을 가지고 있음

  ```java
  String data = "Hi";
  new_data = data.replace(data.charAt(1), 'e');
  System.out.println(data); // "Hi"
  System.out.println(new_data); // "He"
  ```

<br>

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

<br>

#### `contains()`

* 문자열 내에 특정 문자열이 있는지 확인

  ```
  String str = "김혜림은 천재다";
  if(str.contains("김혜림"))
  	System.out.println("있네~~");
  ```

* 있으면 `true`

* 없으면 `false`

<br>

---

<br>

## 문자열을 시간으로

```java
public class BoxOffice {
    private Date openDt; // 개봉일

	public Date toDate(String date) {
        Date dateObj = null;
        SimpleDateFormat format = new SimpleDateFormat("yyyy-MM-dd");
        
        try {
            dateObj = format.parse(date);
        } catch (ParseException e) {
            e.printStackTrace();
            dateObj = new Date();
        }
        return dateObj;
    }
}

```

