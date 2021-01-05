# 파이썬의 자료형

### 0. 종류

- Numeric
- Sequence (list, tuple, range)
- Text Sequence (str)
- Mapping (dict)
- Set (set)
- Bool (True, False, not, and, or(논리), &, |, ~ (비교))
- date, timedate (날짜)

### 1. Numeric

- 숫자로 된 자료형
- 정수형(integer)과 실수형(float)이 있음
  - 8진수형과 16진수형이 있지만 잘 쓰이지 않음
- **Numeric의 연산**
  - `+` : 덧셈, `-` : 뺄셈, `*` : 곱셈, `/`: 나눗셈, `//` : 몫, `%` : 나머지, `**` : 제곱

### 2. Sequence

#### 2.1. list - []

```python
li = [1, 2, 3]
```

- 임의의 값을 순서대로 저장하는 집합 자료형

- 자료구조에서 중요

- 순서 O, 중복 O, 수정 O, 삭제 O
  ```python
  a = [1, 2, 3]
print(a)
  
  # indexing
  print(a[0])
  print(a[1])
  print(a[2])
  # print(a[3])  - IndexError

  # slicing
  print(a[0:2])

  a[0] = 5
  print(a)
  ```
  
  ```
  -- 출력 결과 --
  [1, 2, 3]
  1
  2
  3
  [1, 2]
  [5, 2, 3]
  ```

- 파이썬의 list는 C, Java의 배열과 달리 자료형을 섞어서 넣을 수 있다.

  ```python
  a = [1, 2, 'hello', 3.14]
  b = [1, 2, ['show', 'me', 'the', 'money'], 3.14]
  ```


- **주요 내장 함수**
  - `append(item)` : 리스트 맨 뒤에 item을 추가
  - `insert(idx, item)` : idx 자리에 item을 추가
  - `remove(item)` : 리스트에서 item을 제거
  - `pop()` : 기존 리스트에서 요소를 가져오고 삭제시킨다.
  - `extend(iter)` : 리스트에 iter의 요소를 추가한다.

#### 2.2. tuple - ()

```python
tu = (1, 2, 3)
```

- 읽기 전용 (immutable)

- 순서 O, 중복 O, 수정 X, 삭제 X


- 튜플 내 원소의 개수가 1개인 경우 원소 뒤에 콤마를 붙여야 한다.

  ```python
  a = (1)
  b = (1,)
  print(type(a), type(b))
  ```

  ```
  -- 출력 결과 --
  <class 'int'> <class 'tuple'>
  ```

#### 2.3. range

```python
range(10)			# (0, 1, 2, 3, 4, 5, 6, 7, 8, 9)
range(1, 11)		# (1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
range(1, 11, 2)		# (1, 3, 5, 7, 9)
```

- 숫자의 연속을 나타내며 주로 for 루프에서 특정 횟수만큼 반복하는 데 사용된다.

### 3. Text Sequence (str)

```python
a = 'apple'
b = "banana"	# '', "" 모두 사용 가능
```

- 문자열을 나타내는 자료형

- list처럼 indexing과 slicing이 가능하다.

- **주요 내장 함수**

  - `caplitalize()` : 앞 글자를 대문자로 만드는 함수
  - `replace(oldchar, newchar)` : 문자열 내의 oldchar를 newchar로 바꿈
  - `split(token)` : 문자열을 token 기준으로 쪼개는 함수
  - `strip()` : 문자열 양쪽 공백 제거
    - `lstrip()` : 문자열 왼쪽 공백 제거
    - `rstrip()` : 문자열 오른쪽 공백 제거
  - `endswith(tup)` : 문자열 내에 tup 안의 문자열이 있는지를 확인
  - `count(ch)` : 문자열 내 ch의 빈도

### 4. Mapping type (dict) - {}
```python
fruit_color = {
    'apple': 'red',
    'banana': 'yellow',
    'grape': 'purple',
    'melon': 'green',
    'orange': 'orange'
}
```
- key와 value의 대응관계 자료형
- Hash 또는 Associative array와 유사한 구조
- 순서 X, 키 중복 X, 수정 O, 삭제 O



