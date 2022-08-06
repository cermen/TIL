# Pandas 1일차

### 개요

- 데이터 분석 및 조작을 위해 작성된 파이썬 라이브러리

```python
import pandas as pd
```

### Series 클래스

- 넘파이 1차원 배열과 비슷함
- series = index + value

```python
arr1 = np.array([1,2,3,4,'jyu'] , dtype=np.object)
print(arr1)
```

```
[1 2 3 4 'jyu']
```



```python
arr2 = pd.Series([1,2,3,4,5],
        		 dtype=np.int32,
        		 index = ['강남', '교대', '서초', '방배', '사당'])
print(arr2)
```

```
강남    1
교대    2
서초    3
방배    4
사당    5
dtype: int32
```



```python
arr3 = pd.Series({'a': 3, 'u': 9, 'd': -4, 'i': 2}, dtype=np.float64)
print(arr3)
```

```
a    3.0
u    9.0
d   -4.0
i    2.0
dtype: float64
```

#### fancy indexing & boolean indexing

```python
print(ary[[0,2]])
```

```
a    3.0
d   -4.0
dtype: float64
```



```python
print(ary[ary % 2 == 0])
```

```
d   -4.0
i    2.0
dtype: float64
```



### DataFrame 클래스

- 2차원 배열을 다룸

```python
data = {'name': ['김철수', '이영희', '박영수', '최철희', '홍길동'],
        'birth': [2000, 2001, 2002, 2003, 2004],
        'phone': ['1111-1111', '2222-2222', '3333-3333', '5555-5555', '7777-7777']}
userDF = pd.DataFrame(data)
display(userDF)
```

![](C:\Users\SAMSUNG\Desktop\TIL\Numpy_Pandas\pandas_img\dataframe.PNG)

- DataFrame의 내장 속성과 메서드 
  - `DataFrame.shape`: 열/행 수
  - `DataFrame.size`: 행렬 크기 (열x행)
  - `DataFrame.ndim`: 차원
  - `DataFrame.index` : 인덱스명
  - `DataFrame.columns` : 컬럼명
  - `DataFrame.dtypes` : 각 열의 자료형
  - `DataFrame.info()` : 각 열의 자세한 정보
  - `DataFrame.describe()` : 각 열의 통계 정보
- DataFrame 컬럼 관련 메서드 
  - `DataFrame.column.describe()` : 해당 열의 통계 정보
  - `DataFrame.column.mean()` : 해당 열의 평균 반환
  - `DataFrame.column.unique()` : 해당 열의 값들을 중복을 제거하고 반환
  - `DataFrame.column.value_counts()` : 해당 열의 각 값이 나오는 횟수 반환

#### DataFrame indexing

- DataFrame indexing은 열 우선

```python
print(userDF['name'])
```

```
0    김철수
1    이영희
2    박영수
3    최철희
4    홍길동
Name: name, dtype: object
```



```python
print(userDF['name'][[0,2]])
```

```
0    김철수
2    박영수
Name: name, dtype: object
```

#### Pandas 문자 함수

함수 앞에 `str`

- `str[index]` : 해당 문자열 인덱스에 위치하는 값을 반환
- `str.split(tok)` : 문자열을 `tok `기준으로 나눔
- `str.startswith(s)` : 문자열이 `s`로 시작할 경우 true 반환
- `str.endswith(s)` : 문자열이 `s`로 끝날 경우 true 반환
- `str.contains(s)` : 문자열에 `s`가 있을 경우 true 반환
- `str.replace(a, b)` : 문자열에서 `a` 부분을 `b`로 반환