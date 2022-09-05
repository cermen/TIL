# NumPy 1일차

### Numpy 개요

- 배열을 지원하는 파이썬의 라이브러리
- 행렬 연산, 수치해석 등을 빠르게 할 수 있다.

```python
import numpy as np
```

### ndarray : 배열 자료구조 클래스

- vector : 1차원
- matrix : 2차원 이상
- 차원 : `ndim`, 크기 : `shape`
- 벡터화 연산이 가능

**선언 방법 : `np.array(배열)`**

```python
ary = np.array([0,1,2,3,4,5,6,7,8,9])
matrix = np.array([[0,1,2],[3,4,5]])
```

#### indexing

```python
print(ary[2])			# 2
print(matrix[1,1])		# 4
print(matrix[:,1])		# [1 4]
print(matrix[1, 1:])	# [4 5]
```

##### boolean indexing

```python
odd_even = np.array([0,1,2,3,4,5,6,7,8,9])
idx = np.array([True, False, True, False, True, False, True, False, True, False])
print(odd_even[idx])				# [0 2 4 6 8]
print(odd_even[odd_even % 2 == 0])	# [0 2 4 6 8]
```

##### fencing indexing

```python
data = np.array([1,2,3,4,5,6,7,8,9])
idx = np.array([0,2,4,6,8])
print(data[idx])	# [1 3 5 7 9]
```

#### 배열의 생성과 변형

```python
ary = np.array([0,1,2,3,4,5,6,7,8,9,10,11]).reshape(3, 4)
print(ary)
print(ary.flatten())	# 행렬을 벡터로 변환
```

```
-- 실행 결과 --
[[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]]
[ 0  1  2  3  4  5  6  7  8  9 10 11]
```

- `np.ix()` : 일부 행, 열만 따서 반환

```python
print('np.ix() --->')
print(ary[np.ix_([0,2],[0,2])])

row_idx = np.array([0,2])
col_idx = np.array([0,2])

print(ary[[row_idx]])
print(ary[[row_idx]] [:, col_idx])
```

```
np.ix() --->
[[ 0  2]
 [ 8 10]]
[[ 0  1  2  3]
 [ 8  9 10 11]]
[[ 0  2]
 [ 8 10]]
```

#### 배열의 자료형



- 배열의 자료형은 `배열.dtype`으로 확인할 수 있다.
  ```python
  print(ary.dtype)
  # 출력 결과: dtype('int32')
  ```

- `astype(자료형)` : 배열의 자료형을 바꾸는 함수

  ```python
  print(arr.astype('float64'))
  ```

  ```
  [[ 0.  1.  2.  3.]
   [ 4.  5.  6.  7.]
   [ 8.  9. 10. 11.]]
  ```

#### 배열 생성 시 사용할 수 있는 함수

- `array(배열)` : 해당 배열 반환
- `arange()` : 순서 배열 반환
- `zeros(크기)` : 0(float64)으로 채워진 행렬을 반환
- `ones(크기)` : 1(float64)로 채워진 행렬을 반환
- `zeros_like(행렬)`, `ones_like(행렬)` : 인자의 행렬과 같은 크기의 zeros/ones 행렬 반환
- `empty(크기)` : 빈 행렬를 반환
- `linspace()`

- `행렬.T` : 전치행렬 반환

