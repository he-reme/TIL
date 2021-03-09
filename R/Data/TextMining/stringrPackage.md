# stringr 패키지

> 텍스트 전처리
>
>  정규 표현식 활용

#### stringr 패키지

>다양한 문자열 처리 함수 제공 패키지

```
install.pakages("stringr")
library(stringr)
```

* Detect Matches
  * `str_detect(string, pattern)`
    * 해당 문자열에 pattern이 있는지 확인
    * bool 형식 반환
  * `str_which(string, pattern)`
    * 해당 문자열에서 pattern의 위치 인덱스를 반환
  * `str_count(string, pattern)`
    * 해당 문자열에서 pattern의 갯수 반환
  * `str_locate(string, pattern)`
  * `str_locate_all.str_locate(string, pattern)`
* Subset Strings
  * `str_sub(str, start=1L, end=-1L)`
  * `str_subset(string, pattern)`
  * `str_extract(string, pattern)`
  * `str_match(string, pattern)`
* Manage Lengths
  * `str_length(string)`
  * `str_pad(string, width, side=c("left", "right", "both"), pad="")`
  * `str_trunc(string, width, side=c("right", "left", "center"), ellipsis="...")`
  * `str_trim(string, side=c("both", "left", "right"))`
* Mutate Strings
  * `str_sub()`
  * `str_replace(string, pattern, replacement)`
  * `str_replace_all(string, pattern, replacement)`
  * `str_to_lower(string, locale="en")`
  * `str_to_upper(string, locale="en")`
  * `str_to_title(string, locale="en")`
* Join and Split
  * 등등
* Order Strings
  * `str_order(x, decreasing=F, na_last=T, locale="en", numeric=F, ...)`
  * `str_sort(x, decreasing=F, na_last=T, locale="en", numeric=F, ...)`
* Helpers
  * 등등