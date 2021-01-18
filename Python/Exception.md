# Exception

> 예외
>
> 프로그램 코드는 이상이 없으나 실행 중에 불가피하게 발생하는 문제

* 에러

  * python, javascript, R
    * 구문(신텍스)적으로 잘못된 것이 인식되면 에러를 발생시키고 처리를 종료한다.

* 예외

  * python, javascript

    * 프로그램 코드는 이상이 없으나 실행 중에 불가피하게 발생하는 문제 (약간 가벼운 에러)

    1. 발생한 예외를 처리하는 코드가 준비되어 있는지 확인하고, 준비되어 있는 예외처리 코드를 실행한다.
    2. 예외처리 코드가 준비된 상황이 아니면, 에러를 발생시키고 처리를 종료한다.

  * R

    * ???



---



## 예외 처리

* 기본 구조

  ```python
  try:
  	실행할 명령 (예외가 발생할 가능성이 있는 블록)
  except 예외 as 변수:
  	예외 처리 코드 블록
  else:
  	예외가 발생하지 않았을 때 수행되는 코드 블록
  finally:
      예외 발생 여부와 관계없이 수행되는 코드 블록
  ```

  * 간단하게 `try:` `except:` 까지만 사용 가능

  * `finally` 블록

    * 예외 발생 여부와 무관하게 반드시 실행해야 할 명령 지정

      

---



## 예외 종류

#### (1) `NameError`

* 명칭이 발견되지 않음
* 초기화하지 않은 변수를 사용할 때 발생

#### (2)`ValueError`

* 타입은 맞지만 값의 형식이 잘못됨

#### (3) `ZeroDivisionError`

* 0으로 나눔

#### (4) `IndexError`

* 첨자가 범위를 벗어남

#### (5) `TypeError`

* 타입이 맞지 않음
* 숫자가 필요한 곳에 문자열을 사용한 경우 등

#### (6) 사용 예시1

```python
str = "89"
try:
	score = int(str)
	print(score)
	a = str[5]
except ValueError:
	print("점수의 형식이 잘못되었습니다.")
except IndexError:
	print("첨자 범위를 벗어났습니다.")
print("작업 완료")

''' 
괄호로 묶어 두개 이상 동시 받기 가능!
except (ValueError, IndexError):
	print("점수의 형식이나 첨자가 잘못되었습니다.")
''' 
```

* 결과

  ```
  89
  첨자 범위를 벗어났습니다.
  작업 완료
  ```



## 고의적으로 예외 발생 시키기

#### (1) `rasie` 명령

* 예시

  ```python
  def calcsum(n):
  	if(n<0):
  		raise ValueError
  	sum = 0
  	for i in range(n+1):
  		sum = sum + i
  	return sum
  try:
  	print("~10 =", calcsum(10))
  	print("~-5 =", calcsum(-5))
  except ValueError:
  	print("입력값이 잘못되었습니다.")
  ```

  ```
  ~10 = 55
  입력값이 잘못되었습니다.
  ```



#### (2) `assert` 문장

* `assert 조건, 메시지`
* 프로그램의 현재 상태가 맞는지 확인

* 예시

  ```python
  score = 128
  assert score <= 100, "점수는 100 이하여야 합니다."
  print(score)
  ```

  ```
  # 에러로 인한 종료..
  AssertionError : 점수는 100 이하여야 합니다.
  ```

  