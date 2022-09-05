# Pandas 2일차

### 행 인덱싱, 데이터 조작, 인덱스 조작

#### 행 인덱싱

**`loc()` : 라벨값 기반의 2차원 인덱싱**

```py
sampleDF.loc['a']
```

- 조건을 이용하여 인덱싱할 수 있음

```python
reviews.loc[reviews.country == 'Italy']
```

```python
reviews.loc[(reviews.country == 'Italy') & (reviews.points >= 90)]
```

- 두 개 이상의 컬럼을 이용할 시 `isin()` 사용

```python
reviews.loc[reviews.country.isin(['Italy', 'France'])]
```

**`iloc()` : 순서를 나타내는 정수 기반의 2차원 인덱싱**

```python
sampleDF = pd.DataFrame(np.arange(10, 22).reshape(3,4) , 
                        index   = ['a', 'b', 'c'],
                        columns = ['col01' , 'col02', 'col03', 'col04'] )
```

```python
# 두 구문 모두 같은 값을 출력
print(sampleDF.loc['a'])
print(sampleDF.iloc[0])
```

```python
# 두 구문 모두 11을 출력
print(sampleDF['col02']['a'])
print(sampleDF.loc['a', 'col02'])
print(sampleDF.iloc[0, 1])
```

```python
print(sampleDF.loc['a', 'col01':'col02'])
print(sampleDF.loc['a':'b', 'col01'])
print(sampleDF['col01']['a':'b'])
# print(sampleDF['col01':'col02', 'a']) : 오류
```

#### 데이터 프레임 조작

- `df.count()` : 각 열의 `NaN`이 아닌 행의 개수를 반환
- `df.value_counts()` : 각 값의 개수를 반환
- `df[new_col]` : 새 컬럼 ` new_col` 추가
- `df.drop(label= , axis= , inplace= )` : 해당 컬럼 삭제
- `df.drop_duplicates(subset= )` : subset의 열에서 중복 값을 가진 행 삭제
- `df.set_index()` : 해당 컬럼을 인덱스로 설정
- `df.reset_index()` : 새로운 인덱스 할당, 기존 인덱스는 새로운 컬럼이 된다.
- `df.rename(columns= , index= )` : 행/열의 이름을 바꾼다.
- `df.rename_axis('name', axis=['rows'|'columns'])` : 행/열의 제목을 설정
- 여러개의 복합 조건을 이용해서 불리언 인덱스를 만들어서 작업
  - and -> `&`
  - or -> `|`
  - not -> `!` , `~`

#### 정렬

- `df.sort_index(axis =  , ascending = )` : 인덱스 값 기준 정렬
- `df.sort_values(by = , ascending = )` : 컬럼 값 기준 정렬

