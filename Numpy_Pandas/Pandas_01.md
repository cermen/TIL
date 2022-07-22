# Pandas 1일차

### 개요

- 데이터 분석 및 조작을 위해 작성된 파이썬 라이브러리
- 다음과 같이 선언한다.

```python
import pandas as pd
```

### Series 클래스

- 넘파이 1차원 배열과 비슷함
- series = index + value

**선언법 1**

```python
arr1 = np.array([1,2,3,4,'jyu'] , dtype=np.object)
print(arr1)
```

```
[1 2 3 4 'jyu']
```

**선언법 2**: index 지정

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

**선언법 3**: dict 이용

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

#### Series 주요 속성/함수

- `Series.size` : 원소의 개수(Series의 길이)를 반환
- `Series.shape` : 원소의 개수를 튜플 형태로 반환
- `Series.unique()` : 중복을 제거한 원소들을 반환
- `Series.count()` : NaN을 제외한 개수를 반환
- `Series.mean()` : NaN을 제외한 원소들의 평균을 반환
- `Series.value_counts()` : NaN을 제외한 원소들의 빈도를 반환

#### fancy indexing & boolean indexing

- fancy indexing : Series에서 특정 번째 값만 indexing

```python
print(ary[[0,2]])
```

```
a    3.0
d   -4.0
dtype: float64
```

- boolean indexing : Series에서 True에 해당하는 값만 indexing

```python
print(ary[ary % 2 == 0])
```

```
d   -4.0
i    2.0
dtype: float64
```

#### Series 연산

- Series는 index를 기준으로 연산한다.

```python
s1 = pd.Series([1, 2, 3, 4], ['a', 'b', 'c', 'd'])
s2 = pd.Series([6, 3, 2, 1], ['a', 'b', 'c', 'd'])
print(s1 + s2)
```

```
a    7
b    5
c    5
d    5
dtype: int64
```

- Series의 경우에도 스칼라와의 연산은 브로드캐스팅이 적용된다.

```python
print(s1 ** 2)
```

```
a    1
b    8
c    9
d    4
dtype: int64
```

- index pair가 맞지 않는 경우에는 해당 인덱스에 NaN을 생성한다.

```python
s1 = pd.Series([1, 2, 3, 4], ['a', 'b', 'c', 'd'])
s2 = pd.Series([6, 3, 2, 1], ['a', 'b', 'c', 'e'])
print(s1 + s2)
```

```
a    7.0
b    5.0
c    5.0
d    NaN
e    NaN
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

- DataFrame의 내장 속성과 메서드 
  - `DataFrame.shape`: 열/행 수
  - `DataFrame.size`: 행렬 크기 (열x행)
  - `DataFrame.ndim`: 차원
  - `DataFrame.index` : 인덱스명
  - `DataFrame.columns` : 컬럼명
  - `DataFrame.dtypes` : 각 열의 자료형
  - `DataFrame.info()` : 각 열의 자세한 정보
  - `DataFrame.describe()` : 각 열의 통계 정보

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

- 그러나 slicing은 행을 추출한다.

```python
print(userDF[0:2])
```

```
   name  birth      phone
0  김철수   2000  1111-1111
1  이영희   2001  2222-2222
```

#### Pandas 문자 함수

함수 앞에 `str`

- `str[index]` : 해당 문자열 인덱스에 위치하는 값을 반환
- `str.split(tok)` : 문자열을 `tok `기준으로 나눔
- `str.startswith(s)` : 문자열이 `s`로 시작할 경우 true 반환
- `str.endswith(s)` : 문자열이 `s`로 끝날 경우 true 반환
- `str.contains(s)` : 문자열에 `s`가 있을 경우 true 반환
- `str.replace(a, b)` : 문자열에서 `a` 부분을 `b`로 반환