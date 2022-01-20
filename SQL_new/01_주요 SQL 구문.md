# 주요 SQL 구문

### SELECT 문

테이블에 저장된 데이터를 불러오는 데 쓰인다.

```mysql
SELECT COLUMN_1, COLUMN_2, ...
FROM TABLE_NAME;
```

모든 컬럼을 조회할 때

```mysql
SELECT *
FROM TABLE_NAME;
```

#### ALIAS

- 테이블 등의 이명(異名)
- 가독성을 높임 => SQL 성능 향상

```mysql
select c.first_name, c.last_name, c.email
from customer c;
```

### ORDER BY 문

SELECT문에서 가져온 데이터를 정렬하는 데 사용된다. 업무 처리상 매우 중요한 기능이다.

```mysql
SELECT COLUMN_1, COLUMN_2, ...
FROM TABLE_NAME
ORDER BY COLUMN_1 ASC, COLUMN_2 DESC;
```

이는 다음과 같이 바꿔 쓸 수 있다.

```mysql
SELECT COLUMN_1, COLUMN_2, ...
FROM TABLE_NAME
ORDER BY 1 ASC, 2 DESC;
```

다만 위 방식은 유지보수 등의 측면에서 좋지 않다.

### DISTINCT 문

중복을 제거하는 구문이다.

```mysql
select distinct bcolor
from t1
order by bcolor;

select distinct bcolor, fcolor 
from t1
order by bcolor, fcolor;

select distinct on (bcolor) bcolor, fcolor 
from t1
order by bcolor, fcolor desc;
```

### WHERE 절

집합을 가져올 때 어떤 집합을 가져올 것인지에 대한 조건을 설정하는 절이다.

```mysql
SELECT COLUMN_1, COLUMN_2, ...
FROM TABLE_NAME
WHERE <CONDITION>;
```

### LIMIT 절

- 특정 집합을 출력 시 출력하는 행의 수를 한정하는 역할을 한다.
- MySQL에서 지원한다.

```mysql
SELECT *
FROM TABLE_NAME
LIMIT N;
```

`OFFSET` : 시작 지점을 설정 -> 아래 구문에서 (M+1)번째 행부터 출력

```mysql
SELECT *
FROM TABLE_NAME
LIMIT N
OFFSET M;
```

### FETCH 절

- 특정 집합을 출력 시 출력하는 행의 수를 한정하는 역할을 하며, 부분 범위 처리 시 아용된다.
- `LIMIT` 절과 기능이 동일하며, Oracle에서 지원한다.

```mysql
SELECT *
FROM TABLE_NAME
FETCH FIRST [N] ROW ONLY;

SELECT *
FROM TABLE_NAME
OFFSET M		-- 시작 지점을 설정 -> 아래 구문에서 (M+1)번째 행부터 출력
FETCH FIRST [N] ROW ONLY;
```

### IN 연산자

특정 집합(컬럼 혹은 리스트)에서 특정 집합 혹은 리스트가 존재하는지 판단하는 연산자이다.

```mysql
SELECT *
FROM TABLE_NAME
WHERE COLUMN_NAME IN (VALUE1, VALUE2, ...);
```

#### OR 연산자와의 비교

```mysql
select customer_id , rental_id , return_date 
from rental
where customer_id in (1, 2)
order by return_date desc;

-- 위 SQL문과 같은 결과 출력
select customer_id , rental_id , return_date 
from rental
where customer_id = 1 or customer_id = 2
order by return_date desc;
```

- `IN`이 `OR`보다 알아보기 쉬우며, 가독성이 증가한다.

#### NOT IN

```mysql
select customer_id , rental_id , return_date 
from rental r
where customer_id not in (1, 2)
order by return_date desc;

-- 위 SQL문과 같은 결과 출력
select customer_id , rental_id , return_date 
from rental
where customer_id <> 1 and customer_id <> 2	-- <>은 같지 않음을 뜻한다.
order by return_date desc;
```

### BETWEEN 연산자

특정 집합에서 어떠한 컬럼의 값이 특정 범위 안에 들어가는 집합을 출력하는 연산자이다.

```mysql
SELECT *
FROM TABLE_NAME
WHERE COLUMN_NAME
BETWEEN VALUE_A AND VALUE_B; -- WHERE COLUMN >= VALUE_A AND COLUMN <= VALUE_B

SELECT *
FROM TABLE_NAME
WHERE COLUMN_NAME
NOT BETWEEN VALUE_A AND VALUE_B; -- WHERE COLUMN < VALUE_A OR COLUMN > VALUE_B
```

#### 일자 비교

```mysql
select customer_id , payment_id , amount , payment_date 
from payment
where payment_date between '2007-02-15' and '2007-02-19'
order by payment_date desc;
```

위와 같이 하면 `2007-02-19`까지가 아닌 그 전날인  `2007-02-18`까지만 나온다.
<= timestamp 옆에 날짜만 있으면 시각을 `00:00:00`으로 간주하기 때문이다.

따라서 일자를 비교할 때에는 `cast()` 함수나 `to_char()` 함수를 사용한다.

```mysql
select customer_id , payment_id , amount , payment_date 
from payment
where cast(payment_date as date) between '2007-02-15' and '2007-02-19'
order by payment_date desc;

-- 위 SQL문과 같은 결과 출력
select customer_id , payment_id , amount , payment_date 
from payment
where to_char(payment_date, 'YYYY-MM-DD') between '2007-02-15' and '2007-02-19'
order by payment_date desc;
```

### LIKE 연산자

특정 집합에서 어떠한 컬럼의 값이 특정 값과 유사한 패턴을 갖는 집합을 출력하는 연산자이다.

```mysql
SELECT *
FROM TABLE_NAME
WHERE COLUMN_NAME
LIKE 특정패턴

SELECT *
FROM TABLE_NAME
WHERE COLUMN_NAME
NOT LIKE 특정패턴
```

#### 와일드카드 연산자

- `%` : 글자 수를 정하지 않고 
  - `'foo' like 'f%'` : 참
- `_` : 글자 수를 정하고 
  - `'foo' like '_o_'` : 참
  - `'foo' like 'f_'` : 거짓

### IS NULL 연산자

특정 값 혹은 컬럼이 NULL인지 아닌지를 판단하는 연산자이다.

```mysql
SELECT *
FROM TABLE_NAME
WHERE COLUMN_NAME IS NULL;

SELECT *
FROM TABLE_NAME
WHERE COLUMN_NAME IS NOT NULL;
```

