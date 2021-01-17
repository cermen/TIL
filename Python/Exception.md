# 예외 처리

> 예외(Exception) : 프로그램 코드는 이상이 없으나 실행 중에 불가피하게 발생하는 문제


#### 예외 처리 구문

```python
try:
    # 에러가 발생할 가능성이 있는 코드
except xxxError:
    # 1. 프로그램의 흐름을 정상으로 컨트롤
    # 2. 예외발생의 디버깅
    # 3. 로그파일 만들어서 예외정보를 저장
except xxxError: # 다중으로 처리할 수 있음
    # 발생된 에러를 잡기 위한 객체 정의
else:
    # 에러가 발생되지 않을 때 실행되는 블럭
finally:
    # 무조건 실행
```

- 예시

  ```python
  def user_key_in():
      try:
          age = int(input('본인의 나이를 입력하세요: '))
      except Exception as e:
          print('error =', e)
      else:
          print('age -', age)
          print('함수 실행 종료')
      finally:
          print('finally - 예외 발생 상관 없이 항상 실행')
  
  user_key_in()
  ```
  ```
  본인의 나이를 입력하세요 : 28
  age - 28
  함수 실행 종료
  finally - 예외 발생 상관 없이 항상 실행
  ```
  ```
  본인의 나이를 입력하세요 : jyu
  error = invalid literal for int() with base 10: 'jyu'
  finally - 예외 발생 상관 없이 항상 실행
  ```

- 사용자 정의 예외 클래스를 작성할 수 있다.

  ```python
  class InsufficientError(Exception):
      def __init__(self, msg):
          self.msg = msg
          
  class Account:
      def __init__(self, account, balance, intetest_rate):
          self.account = account
          self.balance = balance
          self.intetest_rate = intetest_rate
  
      def withdraw(self, amount):
          try:
              if self.balance < amount:
                  raise InsufficientError('잔액이 부족합니다.')
          except Exception as e:
              print('error msg -', str(e))
          else:
              self.balance -= amount
              
  account = Account('100', 100000, 0.073)
  account.withdraw(200000)
  print('프로그램 종료')
  ```

  ```
  --- 실행 결과 ---
  error msg - 잔액이 부족합니다.
  프로그램 종료
  ```

  
