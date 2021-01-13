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

### Comprehension

- 다른 sequence로부터 새로운 sequence를 만드는 기능
  - list comprehension : `[출력표현식 for 요소 in sequence [if 조건식]]`
  - set comprehension : `{출력표현식 for 요소 in sequence [if 조건식]}` (python 3.0 이상)
  - dictionary comprehension : `{key:value for 요소 in sequence [if 조건식]}` (python 3.0 이상)

```python
dataset = [4, True, 'jyu', 3.1, 10]

int_type = [value ** 2 for value in dataset if type(value) == int]
print(int_type)

dataset = [1, 1, 2, 2, 3, 3, 4, 4]
set_type = {value * value for value in dataset}
print(set_type)

dataset = {1: 'jyu', 2: 'park', 3: 'multicampus'}

new_set = {value: key for key, value in dataset.items() if key >= 2}
print(new_set)
```

```
--- 실행 결과 ---
[16, 100]
{16, 1, 4, 9}
{'park': 2, 'multicampus': 3}
```

### 제너레이터 (Generator)

- iterator를 만들어주는 기능
- `yield` 키워드 : 메모리 성능 때문에 루프를 컨트롤하기 위해 쓰여지는 루틴
  - 잠시 함수 실행을 멈추고 호출한 곳에 값을 전달
  - 현재 실행된 상태를 계속 유지
  - 그러므로, 다시 해당 함수를 호출하면 현재 실행된 상태를 기반으로 다음 코드를 실행
```python
def text_sequence_func():
    msg = 'hi python'
    for txt in msg:
        yield txt

char_ite = iter(text_sequence_func())
print(next(char_ite))
```

#### Generator Comprehension

- 실제 컬렉션 데이터를 리턴하지 않고, 표현식만 유지
- `(출력형식 for 요소 in collection)`
```python
square_data = (num ** 2 for num in range(5))
for data in square_data:
    print(data, end='\t')
```

### 포함

- 상속을 피하고 클래스의 일부 기능을 그대로 활용하고 싶을 때 사용한다.

```python
class Calc01(object):
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def add(self):
        return self.x + self.y

    def multiply(self):
        return self.x * self.y

class Calc02:
    def __init__(self, x, y):
        self.x = x
        self.y = y
        self.calc01 = Calc01(x, y)   # 객체를 명시적으로 생성

    def add(self):
        return self.x + self.y

    def subtract(self):
        return self.x - self.y

    def multiply(self):
        return self.calc01.multiply()

calc = Calc02(3, 4)
print('calc multiply - ', calc.multiply())
```

```
--- 실행 결과 ---
calc multiply -  12
```

### namedtuple

- 클래스 없이 객체를 생성하는 방법
- `collections` 모듈 내에 정의됨
- `collections.namedtuple('클래스 이름', '변수')`
```python
import collection

# Person = collections.namedtuple('Person', ['name', 'id'])
# Person = collections.namedtuple('Person', 'name id')
Person = collections.namedtuple('Person', 'name, id')
per = Person('jyu', '2320')
print(per, type(per))
```

```
--- 실행 결과 ---
Person(name='jyu', id='2320') <class '__main__.Person'>
```

