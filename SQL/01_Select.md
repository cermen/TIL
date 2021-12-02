# SELECT 구문

### SELECT 구문 템플릿
```sql
SELECT [ 특정컬럼 | *(전체컬럼) | 표현식 | DISTINCT | AS(컬럼별칭) ]
FROM [ 테이블명 | JOIN | SELECT(서브쿼리) ]
[WHERE 조건식 | SELECT(서브쿼리)
GROUP BY 기준컬럼 | SELECT(서브쿼리)
HAVING 조건식
ORDER BY 기준컬럼];
```

* 테이블 전체 출력

  ```sql
  SELECT *
  FROM 테이블명
  ```
  
* 특정 컬럼 출력

  ```sql
  SELECT DISTINCT JOB_ID
  FROM EMPLOYEE;
  ```

### 별칭

- 별칭을 사용하려는 대상 뒤에 `AS 별칭`을 기술 (별칭은 공백으로 구분)
- `AS`는 생략 가능
- 별칭에 특수문자(공백 포함)가 포함된 경우 따옴표를 사용해야 한다.

**사용 예시**

```sql
SELECT 	EMP_NAME AS 이름,
		EMP_NO AS 주민번호,
		SALARY AS "급여(원)",
		DEPT_ID 부서번호 	/* AS 생략 가능 */
FROM EMPLOYEE;
```

### DISTINCT

- 컬럼에 포함된 중복값을 한 번씩만 표시하고자 할 때 사용
```sql
SELECT DISTINCT DEPT_ID
FROM EMPLOYEE;
```

### 연결 연산자 (||)

- 연결 연산자 `||`를 사용하여 여러 컬럼을 하나의 컬럼인 것처럼 연결하거나, 컬럼과 리터럴을 연결할 수 있다.
```sql
SELECT EMP_NAME||'의 월급은 '||SALARY||'원입니다.'
FROM EMPLOYEE;
```

### 논리 연산자

- 여러 개의 제한 조건 결과를 하나의 논리 결과로 만들어준다.
- 종류 : `AND`, `OR`, `NOT`

### 비교 연산자

- 표현식 사이의 관계를 비교하기 위해 사용

- 종류: `=`, `>`, `<`, `>=`, `<=`, `<>`/`!=`/`^=`, `BETWEEN AND`, `LIKE`/`NOT LIKE`, `IS NULL`/`IS NOT NULL`, `IN`

#### BETWEEN AND

- 비교하려는 값이 지정한 범위에 포함되면 TRUE를 반환하는 연산자
```sql
SELECT 	EMP_NAME,
		SALARY
FROM EMPLOYEE
WHERE SALARY BETWEEN 3500000 AND 5500000;
```

#### LIKE

- 비교하려는 값이 지정한 특정 패턴을 만족시키면 TRUE를 반환하는 연산자
- 패턴 지정을 위해 와일드카드 사용
  - `%` : % 부분에는 0개 이상의 임의 문자열이 있다는 의미
  - `_` : % 부분에는 문자 1개만 있다는 의미
```sql
SELECT EMP_NAME, SALARY
FROM EMPLOYEE
WHERE EMP_NAME LIKE '김%';
```

```sql
SELECT EMP_NAME, EMAIL
FROM EMPLOYEE
WHERE EMAIL LIKE '____%';
```

- Escape option : 와일드 카드 문자를 데이터로 처리해야 하는 경우에 사용
```sql
SELECT EMP_NAME, EMAIL
FROM EMPLOYEE
WHERE EMAIL LIKE '___\_%' ESCAPE '\';	/* ESCAPE OPTION에 사용하는 문자는 임의 지정 가능*/
```

##### NOT LIKE

```sql
SELECT 	EMP_NAME,
		SALARY
FROM EMPLOYEE
WHERE EMP_NAME NOT LIKE '김%';	/* 또는 WHERE NOT EMP_NAME LIKE '김%' */
```

#### IS NULL / IS NOT NULL

- NULL 여부를 비교하는 연산자
```sql
SELECT EMP_NAME, DEPT_ID, BONUS_PCT
FROM EMPLOYEE
WHERE DEPT_ID IS NULL
AND BONUS_PCT IS NOT NULL;
```

#### IN

- 비교하려는 값 목록에 일치하는 값이 있으면 TRUE를 반환하는 연산자
```sql
SELECT EMP_NAME, DEPT_ID, SALARY
FROM EMPLOYEE
WHERE DEPT_ID IN ( '60', '90' );
```

#### 상위 N개 데이터 출력

```sql
SELECT EMP_NAME, DEPT_ID, SALARY
FROM EMPLOYEE
WHERE ROWNUM <= number;
```

