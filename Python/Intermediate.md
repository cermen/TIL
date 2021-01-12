# 중급 문법

### 데코레이터 (Decorator)

- 함수 앞뒤에 기능을 추가하는 기법
- 기능이 비슷한 함수 여러 개를 구현하는 데 유용하다.

```python
def outer_func(func):
    def inner_func():
        print('함수 시작했다!')
        func()
        print('함수 끝났다!')
    return inner_func

def user_func():
    print('user_func 함수가 수행되었습니다.')
    
decorator_func = outer_func(user_func)
decorator_func()

# 위 과정을 심플하게 => '@함수명' 이용
@outer_func
def user_func():
    print('user_func 함수가 수행되었습니다.')
    
user_func()
today()
```

### 이터레이터 (Iterator)

- iterable 객체(iterable object)
  - list, set, tuple, dict - (collection)
  - Text sequence
  - `for item in collection`
- iterator
  - 파이썬 모듈이 가지고 있는 내장함수 `iter()`
  - 순차적으로 다음 데이터를 리턴할 수 있는 객체
  - 내장함수 `next()` 사용해서, 순환하는 다음 값을 반환함
```python
user_list = [1, 2, 3, 4, 5]
# print(next(user_list)) # 오류

user_iterator = iter(user_list)
print('type -', type(user_iterator), type(user_list))
print(next(user_iterator))
```
### 제너레이터 (Generator)

- iterator를 만들어주는 기능
- `yield` 키워드 : 메모리 성능 때문에 루프를 컨트롤하기 위해 쓰여지는 루틴
  - 잠시 함수 실행을 멈추고 호출한 곳에 값을 전달
  - 현재 실행된 상태를 계속 유지
  - 그러므로, 다시 해당 함수를 호출하면 현재 실행된 상태를 기반으로 다음 코드를 실행