# 조건문과 반복문

## 조건문

#### if 구문
```python
if 조건식:
    조건식을 만족하는 경우
```

#### if-else 구문
```python
if 조건식:
    조건식을 만족하는 경우
else:
    조건식을 만족하지 않는 경우
```

#### if-elif-else 구문
```python
if 조건식1:
    조건식1을 만족하는 경우
elif 조건식2:
    조건식1을 만족하지 않는 경우 중 조건식2를 만족하는 경우
else:
    조건식1와 조건식2를 모두 만족하지 않는 경우
```

#### if-in 구문

```python
if i in iter:
    iter에 i가 들어있을 경우
```

#### 삼항 연산자

```python
(참일 경우) if 조건식 else (거짓일 경우)
```



## 반복문

#### while 문

```python
while 조건문:	# 조건이 만족하는 동안 아래 명령문을 반복 실행
	실행 문장
```

#### for 문

```python
for item in collection:	# collection 요소 순서대로 반복하면서 루프 명령 실행
    실행 문장
```

##### 사용 예시

- ```python
  user_sum = 0
  for tmp in range(1, 11, 2):
      print(tmp)
      user_sum += tmp
  print('누적 값은 {}입니다.'.format(user_sum))
  ```

- ```python
  word_list = ['I', 'am', 'studying', 'Python', 'language', 'Yeah']
  for word in word_list:
      if len(word) >= 5:
          print(word)
  ```

- ```python
  user_dict = {'name': 'cermen', 'gender': 'M'}
  for (key, value) in user_dict.items():
      print("{}, {}".format(key, value))
  ```

#### break

- 해당 조건식을 만족하는 경우 반복문을 빠져나감
```python
for i in range(10):	# i가 4일 때까지만 실행됨
    if i == 5:
        break
    print(i, end=' ')
```
```
-- 실행 결과 --
0 1 2 3 4
```

#### continue

- 해당 조건식을 만족하는 경우 다음 차례로 넘김
```python
for i in range(10):	# i가 4일 때 실행되지 않음
    if i == 5:
        continue
    print(i, end='\n')
```

```
-- 실행 결과 --
0 1 2 3 4 6 7 8 9
```

#### enumerate

- 인덱스값과 요소값을 묶는 함수
```python
subject = ['국어', '수학', '영어']
print(list(enumerate(subject)))
```

```
-- 실행 결과 --
[(0, '국어'), (1, '수학'), (2, '영어')]
```

- 반복문에서의 사용

  ```python
  book_list = ['Python', 'C', 'C++', 'Java', 'JavaScript']
  for idx, book in enumerate(book_list):
      print('index - {}, value - {}'.format(idx, book))
  ```

  ```python
  index - 0, value - Python
  index - 1, value - C
  index - 2, value - C++
  index - 3, value - Java
  index - 4, value - JavaScript
  ```