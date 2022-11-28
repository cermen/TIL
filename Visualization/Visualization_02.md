# 데이터 시각화 3일차

### Seaborn plot

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

- `regplot()` : 선점도 - 선형회귀분석 위한 회귀선을 나타내주는 함수
  - 연속변수의 수치형

```python
sns.set_style('dark')

fig = plt.figure(figsize=(15, 5))

area01 = fig.add_subplot(1, 2, 1)
sns.regplot(x='age', y='fare', data=titanic_datasets, ax=area01)

area02 = fig.add_subplot(1, 2, 2)
sns.regplot(x='age', y='fare', data=titanic_datasets, ax=area02, fit_reg=False)

plt.show()
plt.close()
```

- `distplot()` : 히스토그램/커널 밀도 그래프

```python
sns.set_style('dark')

fig = plt.figure(figsize=(15, 5))

area01 = fig.add_subplot(1, 3, 1)
sns.distplot(titanic_datasets['fare'], ax=area01)

area02 = fig.add_subplot(1, 3, 2)
sns.distplot(titanic_datasets['fare'], hist=False, ax=area02)

area03 = fig.add_subplot(1, 3, 3)
sns.distplot(titanic_datasets['fare'], kde=False, ax=area03)

plt.show()
plt.close()
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

- `jointplot()` : 기본적으로 산점도, x-y축에 각 변수에 대한 히스토그램을 동시에 보여준다.

```python
# kind 속성 : reg, hex, kde
sns.jointplot(x='sepal_length', y='sepal_width', data=iris_datasets, kind='reg')
plt.show()
plt.close()
```

- `pairplot()` : 상관관계를 시각화하기 위한 함수

```python
sns.pairplot(iris_datasets, hue='species', markers=['o', 's', 'D'])
plt.show()
plt.close()
```

- `scatterplot()` : 산점도 그리기

```python
sns.scatterplot(data=candy_data, x='sugarpercent', y='winpercent')
plt.show()
plt.close()
```

