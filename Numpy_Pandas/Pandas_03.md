# Pandas 3일차

### `apply()` 함수

- lambda 식과 같이 사용한다
- 행이나 열 단위로 복잡한 데이터 가공이 필요한 경우
- `apply` 함수는 인자로 함수를 넘겨 받을 수 있다

**예시**

```python
func = lambda x : x.max() - x.min()
sampleDF['최대-최소'] = sampleDF.apply(func, axis=1)
```


### `NaN` 관련 함수

- `isnull()`, `isna()` : 각 원소에 대하여 NaN이면 `True`, 아니면 `False`를 반환한다.
- `notnull()`, `notna()` : 각 원소에 대하여 NaN이면 `False`, 아니면 `True`를 반환한다. (`isnul`l/`isna`의 반대)
- `fillna(val)` : NaN 값을 원하는 값으로 변경한다.
- `dropna()` : NaN이 포함된 행을 삭제한다.

### 프레임 인덱스 조작하는 방법

- `set_index(col)` : 해당 컬럼을 인덱스로 설정
- `reset_index()` : 새로운 인덱스 할당 , 기존 인덱스는 index라는 새로운 컬럼으로 추가된다.

### 데이터 프레임 합치기

- `merge(df1, df2, on= , how= )` 
  두 데이터프레임을 키(`on` 속성)에 따라 합병한다.
  - `how` 속성
    - `inner` : inner join과 같은 기능
    - `left` :  left join과 같은 기능
    - `right` : right join과 같은 기능
    - `outer` : outer join과 같은 기능
- `concat([df1, df2, ...], axis= , join= )` 
  데이터프레임을 컬럼(`axis=0`)/인덱스(`axis=1`)에 따라 이어붙인다.
- `join(df, how= )` 
  `merge` 함수와 기능이 같지만 `merge`와는 달리 행 인덱스를 기준으로 결합한다.

### 그룹 분석 및 피봇

- 분할(split) : 데이터를 특정 조건에 의해 분할
- 적용(apply) : 데이터를 집계, 변환, 필터링하는데 필요한 함수를 적용
- 결합(combine) : 적용단계의 처리결과를 하나로 결합

#### `groupby()` 함수

- 특정 컬럼을 기준으로 범주화(grouping)한다.

```python
# 학과 컬럼을 기준으로 범주화
dept_series = df.groupby(df['학과'])

# 학과가 '컴퓨터'인 행만 뽑음
dept_series.get_group('컴퓨터')

# 학과별 각 컬럼의 평균
dept_series.mean()

# 여러 함수를 실행
dept_series.agg([np.mean, np.sum])
```

