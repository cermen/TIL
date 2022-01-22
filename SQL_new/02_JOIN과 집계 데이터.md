# 조인과 집계 데이터

## 조인

### 조인이란?

> 2개 이상의 테이블에 있는 정보 중 사용자가 필요한 집합에 맞게 가상의 테이블처럼 만들어서 겨로가를 보여주는 것이다.

- INNER 조인 : 특정 컬럼을 기준으로 정확히 매칭된 집합을 출력한다.
- OUTER 조인 : 특정 컬럼을 기준으로 정확히 매칭된 집합을 출력하지만 한쪽의 집합은 모두 출력하고 다른 한쪽의 집합은 매칭되는 컬럼의 값만을 출력한다.
- SELF 조인 : 동일한 테이블끼리의 특정 컬럼을 기준으로 매칭되는 집합을 출력한다.
- FULL OUTER 조인 : INNER, LEFT OUTER, RIGHT OUTER 조인 집합을 모두 출력한다.
- CROSS 조인 : 조인되는 두 테이블에서 곱집합을 반환한다.
- NATURAL 조인 : 특정 테이블의 같은 이름을 가진 컬럼 간의 조인집합을 출력한다.

### INNER 조인

특정 컬럼을 기준으로 정확히 매칭된 집합을 출력한다.

```mysql
select 
	c.customer_id , c.first_name , c.last_name , c.email , 
	p.amount , p.payment_date 
from customer c
inner join payment p 
on c.customer_id = p.customer_id
```

```mysql
-- 테이블 3개 조인
select 
	c.customer_id , c.first_name , c.last_name , c.email , 
	p.amount , p.payment_date ,
	s.first_name as staff_first_name , s.last_name as staff_last_name
from customer c
inner join payment p 
on c.customer_id = p.customer_id
inner join staff s 
on p.staff_id = s.staff_id ;
```

### OUTER 조인

특정 컬럼을 기준으로 정확히 매칭된 집합을 출력하지만 한쪽의 집합은 모두 출력하고 다른 한쪽의 집합은 매칭되는 컬럼의 값만을 출력한다.

#### LEFT OUTER

왼쪽 집합만 모두 출력한다.

```mysql
select a.id , a.fruit , b.id , b.fruit 
from basket_a a
left join basket_b b
on a.fruit = b.fruit;

-- 오른쪽이 NULL인 것만 출력
select a.id , a.fruit , b.id , b.fruit 
from basket_a a
left join basket_b b
on a.fruit = b.fruit 
where b.id is null;
```

#### RIGHT OUTER

오른쪽 집합만 모두 출력한다.

```mysql
select a.id , a.fruit , b.id , b.fruit 
from basket_a a
right join basket_b b
on a.fruit = b.fruit;

-- 왼쪽이 NULL인 것만 출력
select a.id , a.fruit , b.id , b.fruit 
from basket_a a
right join basket_b b
on a.fruit = b.fruit 
where a.id is null;
```

### SELF 조인

같은 테이블끼리 특정 컬럼을 기준으로 매칭되는 컬럼을 출력하는 조인이다.

- 사용 목적 : 동일한 테이블이지만 각각의 다른 집합으로 구성해 놓고, 그 다음 그 안에서 자신이 원하는 정보를 추출한다.

```mysql
select
	e.first_name || ' ' || e.last_name employee,
	m.first_name || ' ' || m.last_name manager
from employee e 
[inner|left|right] join employee m
on m.employee_id = e.manager_id
order by manager;
```

### FULL OUTER 조인

INNER, LEFT OUTER, RIGHT OUTER 조인 집합을 모두 출력하는 조인 방식이다.

```mysql
select 
	a.id id_a, a.fruit fruit_a, 
	b.id id_b, b.fruit fruit_b
from basket_a a
full outer join basket_b b
on a.fruit = b.fruit;
```

```mysql
-- 한 쪽이 NULL인 것만 출력
select 
	a.id id_a, a.fruit fruit_a, 
	b.id id_b, b.fruit fruit_b
from basket_a a
full outer join basket_b b
on a.fruit = b.fruit
where a.id is null or b.id is null; 
```

### CROSS 조인

두 개의 테이블의 곱집합 연산(Cartesian Product)의 결과를 출력한다.

```mysql
select *
from cross_t1
cross join cross_t2
order by label;

-- CROSS 조인을 표현하는 다른 방법
select *
from cross_t1 , cross_t2 
order by label;
```

- `ON` 조건이 없다.

### NATURAL 조인

- INNER 조인의 다른 SQL 작성 방식으로, 조인 컬럼을 명시하지 않아도 된다.
- *실무에서 많이 쓰이지 않지만,* 이를 통해 INNER 조인을 더 이해할 수 있다.

```mysql
select *
from products p 
natural join categories c
```

이는 아래 SQL문의 결과와 동일하다.

```sql
select p.category_id , p.product_id , p.product_name , c.category_name 
from products p 
inner join categories c
on p.category_id = c.category_id ;
```

```sql
select p.category_id , p.product_id , p.product_name , c.category_name 
from products p, categories c
where p.category_id = c.category_id ;
```

- 두 테이블 간에 동일한 이름의 컬럼이 두 개 이상 존재하는 경우 결과값이 나오지 않는다.
  => 실무에 많이 쓰이지 않음

## 집계 데이터

### GROUP BY 절

SELECT 문에서 반환된 행을 그룹으로 나누며, 각 그룹에 대한 합계, 평균, 갯수 등을 계산할 수 있다.

```mysql
SELECT COLUMN_1, 집계함수(COLUMN_2)
FROM TABLE_A
GROUP BY COLUMN_1
```

```mysql
-- 단순 GROUP BY
select customer_id
from payment
group by customer_id;

-- 아래 SQL문의 실행 결과와 같음
select distinct customer_id 
from payment;
```

```mysql
-- 거래액이 가장 많은 고객 순으로 출력
select
	customer_id ,
	sum(amount) as amount_sum
from
	payment
group by customer_id
order by amount_sum desc;

-- 실행 결과 같음
select
	customer_id ,
	sum(amount) as amount_sum
from
	payment
group by customer_id
order by 2 desc;
```

```mysql
select 
	s.first_name || ' ' || s.last_name as staff_name,
	pc.count
from staff s
inner join (select
	staff_id ,
	count(payment_id) as count
from
	payment
group by staff_id) pc
on s.staff_id = pc.staff_id;
```

### HAVING 절

GROUP BY 절과 함께 HAVING 절을 사용하여 GROUP BY의 결과를 특정 조건으로 필터링하는 기능을 한다.

```mysql
SELECT COLUMN_1, 집계함수(COLUMN_2)
FROM TABLE_A
GROUP BY COLUMN_1
HAVING 조건식;
```

**WHERE 절과의 차이**

- HAVING 절은 GROUP BY 절에 의해 생성된 그룹행의 조건을 설정한다.
- 반면에 WHERE 절은 GROUP BY 절이 적용되기 전에 개별 행의 조건을 설정한다.

```mysql
-- 예시
select
	customer_id ,
	sum(amount) as amount_sum
from
	payment
group by customer_id
having sum(amount) >= 200;
```

### GROUPING SET 절

GROUPING SET 절을 사용하여 여러 개의 UNION ALL을 이용한 SQL과 같은 효과를 도출할 수 있다.

```mysql
SELECT C1, C2, 집계합수(C3)
FROM TABLE_A
GROUP BY
GROUPING SETS
(
    (C1, C2),
    (C1),
    (C2),
);
```

### ROLL UP 절

지정된 GROUPING 컬럼의 소계를 생성하는 데 사용된다. 

```mysql
SELECT C1, C2, C3, 집계함수(C4)
FROM TABLE_A
GROUP BY
ROLLUP (C1, C2, C3);

-- 부분 ROLLUP 가능
SELECT C1, C2, C3, 집계함수(C4)
FROM TABLE_A
GROUP BY C1
ROLLUP (C2, C3);
```

### CUBE 절

```mysql
SELECT C1, C2, C3, 집계함수(C4)
FROM TABLE_A
GROUP BY
CUBE (C1, C2, C3);

-- 부분 CUBE 가능
SELECT C1, C2, C3, 집계함수(C4)
FROM TABLE_A
GROUP BY C1
CUBE (C2, C3);
```

- `CUBE(C1, C2, C3)`은 다음과 같다.

```mysql
GROUPING SETS (
    (C1,C2,C3),
    (C1,C2),
    (C1,C3),
    (C2,C3),
    (C1),
    (C2),
    (C3),
    ()
)
```

### 분석 함수

- 특정 집합 내에서 결과 건수의 변화 없이 해당 집합 안에서 합계 및 카운트 등을 계산할 수 있는 함수
- 분석 함수는 집계의 결과 및 집합을 함께 출력한다.

**예시**

```mysql
SELECT COUNT(*) OVER(), A.*
FROM PRODUCT A;
```

#### 문법

```mysql
SELECT 
	C1,
	분석함수(C2, C3, ...) OVER (PARTITION BY C4 ORDER BY C5)
FROM TABLE_A;
```

- 사용하고자 하는 분석함수를 쓰고 대상 컬럼을 기재 후 PARTITION BY에서 값을 구하는 기준 컬럼을 쓰고 ORDER BY에서 정렬 컬럼을 기재한다.

#### AVG() 함수

특정 집합 내에서 결과 건수의 변화 없이 해당 집합 안에서 특정 컬럼의 평균을 구하는 함수이다.

```mysql
select pg.group_name, avg(price)
from product p
inner join product_group pg
on p.group_id = pg.group_id
group by pg.group_name;
```

```mysql
select 
	p.product_name ,
	p.price ,
	pg.group_name ,
	avg(p.price) over (partition by pg.group_name) -- 위 SQL문의 결과를 컬럼으로 출력
from product p
inner join product_group pg 
on p.group_id = pg.group_id;
```

#### 순위 함수

특정 집합 내에서 결과 건수의 변화 없이 해당 집합 안에서 특정 컬럼의 순위를 구하는 함수이다.

- `ROW_NUMBER()` 함수 : 무조건 1, 2, 3, 4...

```sql
select 
	p.product_name ,
	p.price ,
	pg.group_name ,
	row_number() over (partition by pg.group_name order by p.price desc)
from product p
inner join product_group pg 
on p.group_id = pg.group_id;
```

- `RANK()` 함수 : 중복되는 경우 같은 순위로 표기하고 다음 순위 건너뒴

```sql
select 
	p.product_name ,
	p.price ,
	pg.group_name ,
	rank() over (partition by pg.group_name order by p.price desc)
from product p
inner join product_group pg 
on p.group_id = pg.group_id;
```

- `DENSE_RANK()` 함수 : 중복되는 경우 같은 순위로 표기하고 다음 순위로 건너뛰지 않음

```sql
select 
	p.product_name ,
	p.price ,
	pg.group_name ,
	dense_rank () over (partition by pg.group_name order by p.price desc)
from product p
inner join product_group pg 
on p.group_id = pg.group_id;
```

#### FIRST_VALUE, LAST_VALUE 함수

특정 집합 내에서 결과 건수의 변화 없이 해당 집합 안에서 특정 컬럼의 첫 번째 값 혹은 마지막 값을 구하는 함수이다.

```sql
select 
	p.product_name ,
	pg.group_name ,
	p.price ,
	first_value (p.price) over (partition by pg.group_name order by p.price desc)
	as lowest_price_per_group
from product p
inner join product_group pg 
```

```sql
select 
	p.product_name ,
	pg.group_name ,
	p.price ,
	last_value (p.price) over 
	(partition by pg.group_name order by p.price
	range between unbounded preceding and unbounded following)
	as highest_price_per_group
from product p
inner join product_group pg 
on p.group_id = pg.group_id;
```

#### LAG, LEAD 함수

- `LAG` 함수 : 이전 행의 값을 찾는다.
- `LEAD` 함수 : 다음 행의 값을 찾는다.