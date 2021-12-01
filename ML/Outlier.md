## 이상치 처리

```python
# 3분위수, 1분위수
quantile75 = outlierDF.quantile(q=0.75)
quantile25 = outlierDF.quantile(q=0.25)

# IQR(InterQuartile Range)
iqr = quantile75 - quantile25

# lower fence(최저 한계치), upper fence(최고 한계치)
lower_fence = quantile25 - 1.5 * iqr
upper_fence = quantile75 + 1.5 * iqr

# 극단치 경계값
lower_outlier = outlierDF[outlierDF > lower_fence].min()
upper_outlier = outlierDF[outlierDF < upper_fence].max()

# hwy 연비의 이상치 데이터 추출
hwy_outlier_df = dataDF.query('hwy > ' + str(upper_outlier['hwy']))
# cty 연비의 이상치 데이터 추출
cty_outlier_df = dataDF.query('cty > ' + str(upper_outlier['cty']))

outlier_clean_df = dataDF.copy()

# cty 연비에 대한 이상치를 결측값으로 변경
for idx in cty_outlier_df.index:
    outlier_clean_df.loc[idx, 'cty'] = np.nan
# hwy 연비에 대한 이상치를 결측값으로 변경
for idx in hwy_outlier_df.index:
    outlier_clean_df.loc[idx, 'hwy'] = np.nan

# 제거
resultDF = outlier_clean_df.filter(['drv', 'cty', 'hwy']).dropna().groupby('drv').mean()
```

