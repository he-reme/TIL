# StringBuilder

* String은 불변성을 가지고 있기 때문에 계속 문자열을 생성해주면 메모리에 안좋다

* 여러개를 출력할 때 StringBuilder를 사용하면 좋음!

<br>

---

<br>

#### 사용

```c#
using System.Text;

StringBuilder sb = new StringBuilder();
sb.Append("원하는 문자열");
sb.AppendLine("원하는 문자열");
Console.WriteLine(sb.ToString());
```

