# 함수

코드의 중복을 막아 가독성을 높이는 기능을 한다.

```python
def 함수명(매개변수):
    실행할 구문
    return 반환값	
```

#### 파이썬 함수의 특징

- default parameter 사용 가능
  
  ```python
  def add_num(num1, num2, num3=0):
	return num1 + num2 + num3
  
  print(add_num(3, 4))
  print(add_num(3, 4, 5))
  ```
  ```
  --- 실행 결과 ---
  7
  12
  ```

- 함수를 인자로 받을 수 있음

### 전역변수와 지역변수

- 지역변수 : 함수 내부에서 선언하는 변수
- 전역변수 : 함수 바깥에서 선언하는 변수
```python
tmp = 100

def my_func(x):
    tmp += x
    return tmp

print(my_func(100))	# 실행 결과 
```
my_func 함수 외부의 `tmp`와 함수 내부의 `tmp`는 다르게 인식되며, 함수 내부의 `tmp`가 선언 전에 사용되었기 때문에 오류가 발생한다. 따라서 원하는 값을 얻으려면 변수 앞에 `global`을 불여서 `tmp`가 전역 변수임을 알려줘야 한다.
```python
def my_func(x):
    global tmp
    tmp += x
    return tmp
```



### 가변 인수

- 고정되지 않은 임의 개수의 인수를 받음
- `*args`로 표기
```python
def print_words(*word_list):
    for word in word_list:
        print(word)

print_words('one', 'two', 'three', 'four')
```

#### - 키워드 가변 인수

- 인수의 이름과 값의 쌍을 사전으로 만들어 전달한다.
- `**kwargs`로 표기
```python
def print_dict(**di):
    for key, value in di.items():
        print('{} = {}'.format(key, value))

print_dict(name='jyu', birthday='1994-04-20')
```

### 중첩 함수

- 함수 안에 함수가 들어 있는 형태
```python
def outer_func(outer_num):
    def inner_func(num):
        print('inner_func -', num)
    inner_func(outer_num + 100)

outer_func(100)
# inner_func(100) -  내부 함수는 외부 함수 바깥에서 호출할 수 없다.
```

- 활용 예
  - outer 함수 : 자료 생성, inner 함수 포함
  - innet 함수 : 자료 연산/처리(합계, 평균)
  ```python
  def calc_func(data):
      dataset = data

      def sum_func():
        	total = sum(dataset)
        	return total
    	def avg_func(total):
        	avg = total / len(dataset)
        	return avg
    	return sum_func, avg_func
  
  data = list(range(1, 101))
  
  rtn_sum_func, rtn_avg_func = calc_func(data)
  tot = rtn_sum_func()
  avg = rtn_avg_func(tot)
  print(tot, avg)
  ```

### 재귀함수
- 함수 내부에서 자신의 함수를 반복 호출하는 기법
- 용도 : 반복적으로 변수를 변경해서 연산할 때 (누적, 팩토리얼)

```python
def count_func(n):
    if n == 0:
        print('count_func(0) 함수 실행 - 재귀 종료')
    else:
        print('count_func(%d) 함수 호출' % n)
        count_func(n - 1)
        print('count_func(%d) 함수 반환' % n)

count_func(3)
```

```
-- 실행 결과 --
count_func(3) 함수 호출
count_func(2) 함수 호출
count_func(1) 함수 호출
count_func(0) 함수 실행 - 재귀 종료
count_func(1) 함수 반환
count_func(2) 함수 반환
count_func(3) 함수 반환
```

### 람다(lambda) 함수

- 즉시 실행 함수로, 가독성 향상, 코드 간결, 메모리 절약 등의 효과가 있다.

```python
# def multi_func(x, y):
#     return x * y
# 위 multi_func 함수와 같은 기능을 함
lambda_var = lambda x, y: x * y
print(lambda_var(10, 20))
```

