# 데이터 시각화 1~2일차

### plot 유형

- line plot : 꺾은선 그래프

```python
plt.figure(figsize=(15, 5))

plt.plot(to_seoul.index, to_seoul.values, marker='o', label='서울 전입 인구')
plt.plot(to_gyeonggi.index, to_gyeonggi.values, marker='o', label='경기 전입 인구')
plt.title('서울, 경기 전입 인구 변천(1970-2017)', size=20)
plt.xlabel('연도', size=15)
plt.ylabel('전입 인구(명)', size=15)
plt.xticks(rotation=60)
plt.legend(loc='best')

plt.show()
plt.close()
```

- bar plot : 막대 그래프

```python
xlabel = ['1등실', '2등실', '3등실']
plt.figure()
plt.bar(X, Y)

plt.title('bar plot')
plt.xlabel('선실등급')
plt.ylabel('생존자 수')

plt.xticks(X, xlabel)
plt.yticks(Y)

plt.show()
plt.close()
```

```python
plt.figure()

iris_mean_df.plot(kind='bar',
                figsize=(10, 5))

plt.title('각 변수별 평균', size=20)
plt.xlabel('변수', size=15)
plt.ylabel('평균', size=15)

plt.show()
plt.close()
```

- box chart : 최댓값, 최솟값, 중위값, 1/4값, 3/4값 표시

```python
plt.figure()

boxDF.boxplot(by='Y')

plt.title('각 종별 SL 분포')
plt.xlabel('type')
plt.ylabel('cm')

plt.show()
plt.close()
```

- pie chart : 카테고리별 값의 상대적인 비교

```python
labels = ['짬뽕', '순대국밥', '비빔밥', '생고기', '핫도그']
datas = [15, 15, 20, 25, 25]
colors = ['orange', 'blue', 'red', 'yellow', 'green']

plt.figure()

plt.pie(datas, labels=labels, colors=colors, shadow=True, autopct='%1.1f%%')

plt.show()
plt.close()
```

- histogram : 구간에 대한 데이터 집계
	- 변수가 하나인 단변수 데이터의 빈도 수 시각화할 때

```python
datas = np.random.randn(1000)

plt.figure()

plt.hist(datas, bins=100)

plt.show()
plt.close()
```

