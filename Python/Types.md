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

- 임의의 값을 순서대로 저장하는 집합 자료형

- index 부여와 값 변경이 가능하다.
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

  

#### 2.2. tuple - ()

- list와 달리 값 변경이 불가능하다.

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

