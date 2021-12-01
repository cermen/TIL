# Pandas 4일차

- `agg(func)` 함수 : 



- `transform()` : 그룹별 개선된 동일하지만 데이터프레임 자체를 변환
- `cut()` : 동일 길이로 나우어서 범주를 만들고 그룹에 대한 통계량
- `qcut()` : 동일 개수로 나우어서 범주를 만들고 그룹에 대한 통계량



### pivot

- `pivot(Index, columns, value)`
- `pivot_table(data, values, index, columns, aggfunc='mean')`