# 데이터 시각화 - Seaborn

### Seaborn plot

#### 추이 그래프

- `lineplot()` : 시간별 추이를 나타낼 때 쓰는 차트

```python
sns.set_style('dark')

fig = plt.figure(figsize=(8, 5))

sns.lineplot(data=flights, x='month', y='passengers')
plt.show()
```

#### 관계 그래프

- `barplot()` : 카테고리 값에 따른 숫자값의 평균과 편차를 표시하는 차트
  - 평균은 막대의 높이, 편차 에러바

```python
# darkgrid, whilegrid, dark, white, ticks
sns.set_style('dark')

fig = plt.figure(figsize=(15, 5))

# 선실등급에 빈도를 확인하고 싶다면
area01 = fig.add_subplot(1, 3, 1)
area01.set_title('survived - sex')
sns.barplot(x='sex', y='survived', data=titanic_datasets, ax=area01)

area02 = fig.add_subplot(1, 3, 2)
sns.barplot(x='sex', y='survived', hue='class', data=titanic_datasets, ax=area02)

area03 = fig.add_subplot(1, 3, 3)
sns.barplot(x='sex', y='survived', hue='class', dodge=False, palette='Set2', data=titanic_datasets, ax=area03)

plt.show()
```

- `heatmap()` : x, y 범주형
  - 매트릭스 형태로 데이터를 경유

```python
# 피벗테이블로 범주형 변수를 각각 행, 열로 재구분하여
# 성별에 따른 선실등급
table = titanic_datasets.pivot_table(index=['sex'], columns=['class'], aggfunc='size')

sns.heatmap(table, cbar=True, annot=True, fmt='d', linewidths=0.5)

plt.show()
plt.close()
```

- `scatterplot()` : 산점도 그리기

```python
sns.scatterplot(data=candy_data, x='sugarpercent', y='winpercent')
plt.show()
plt.close()
```

- `countplot()` : 카테고리 값별로 데이터 빈도를 표시하는 차트

```python
sns.set_style('dark')

fig = plt.figure(figsize=(15, 5))

# 선실등급에 빈도를 확인하고 싶다면
area01 = fig.add_subplot(1, 3, 1)
area01.set_title('class count')
sns.countplot(x='class', data=titanic_datasets, ax=area01)

area02 = fig.add_subplot(1, 3, 2)
sns.countplot(x='class', hue='who', data=titanic_datasets, ax=area02)

area03 = fig.add_subplot(1, 3, 3)
sns.countplot(x='class', hue='who', dodge=False, palette='Set3', data=titanic_datasets, ax=area03)

plt.show()
plt.close()
```

- `regplot()` : 선형 회귀분석을 위한 회귀선을 나타내주는 함수

```python
sns.set_style('dark')

fig = plt.figure(figsize=(15, 5))

area01 = fig.add_subplot(1, 2, 1)
sns.regplot(data=iris_datasets, x='sepal_length', y='petal_length', ax=area01)

area02 = fig.add_subplot(1, 2, 2)
sns.regplot(data=iris_datasets, x='sepal_length', y='petal_length', ax=area02, fit_reg=False)	# 회귀선 해제

plt.show()
plt.close()
```

- `	lmplot()` : 카테고리 값별로 회귀선을 그릴 때 사용한다.

```python
sns.set_style('dark')

fig = plt.figure(figsize=(15, 5))

sns.lmplot(data=iris_datasets, x='sepal_length', y='petal_length', hue='species')

plt.show()
plt.close()
```

- 범주형 데이터의 분포도
  - `stripplot()` : 데이터 포인트가 중복되어 그려짐
  - `swarmplot()` : 데이터 포인트가 중복되지 않도록 그려짐

```python
sns.set_style('dark')

fig = plt.figure(figsize=(15, 5))

area01 = fig.add_subplot(1, 2, 1)
sns.stripplot(x='class', y='age', data=titanic_datasets, ax=area01)

area02 = fig.add_subplot(1, 2, 2)
sns.swarmplot(x='class', y='age', data=titanic_datasets, ax=area02)

plt.show()
plt.close()
```

#### 분포 그래프

- `histplot()` : 히스토그램 그래프

```python
sns.set_style('dark')

fig = plt.figure(figsize=(7, 5))

sns.histplot(titanic_datasets['age'])

plt.show()
plt.close()
```

- `kdeplot()` : 확률밀도함수 그래프

```python
sns.set_style('dark')

fig = plt.figure(figsize=(7, 5))

sns.kdeplot(data=titanic_datasets, x='age')

plt.show()
plt.close()
```

- `distplot()` : `histplot`과  `kdeplot`의 기능을 모두 제공하는 그래프

```python
sns.set_style('dark')

fig = plt.figure(figsize=(15, 5))

area01 = fig.add_subplot(1, 3, 1)
sns.distplot(titanic_datasets['fare'], ax=area01)

area02 = fig.add_subplot(1, 3, 2)
sns.distplot(titanic_datasets['fare'], hist=False, ax=area02)	# 곡선만 표시

area03 = fig.add_subplot(1, 3, 3)
sns.distplot(titanic_datasets['fare'], kde=False, ax=area03)	# 히스토그램만 표시

plt.show()
plt.close()
```

- `jointplot()` : 산점도와 x-y축 각 변수에 대한 히스토그램을 동시에 보여준다.

```python
# kind 속성 : reg, hex, kde
sns.jointplot(x='sepal_length', y='sepal_width', data=iris_datasets, kind='reg')
plt.show()
plt.close()
```

- `pairplot()` : 각 컬럼 간의 상관관계를 시각화하기 위한 함수

```python
sns.pairplot(iris_datasets, hue='species', markers=['o', 's', 'D'])
plt.show()
plt.close()
```
