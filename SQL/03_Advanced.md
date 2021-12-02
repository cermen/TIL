# SELECT 심화

### ORDER BY

- SELECT 구문 실행 결과를 특정 컬럼 값 기준으로 정렬할 때 사용

```sql
SELECT EMP_NAME, HIRE_DATE, DEPT_ID
FROM EMPLOYEE
WHERE HIRE_DATE > TO_DATE('20030101','YYYYMMDD')
ORDER BY DEPT_ID DESC, HIRE_DATE, EMP_NAME;
```

### GROUP BY

- GROUP BY 절에 기술한 컬럼이나 표현식을 기준으로 데이터 그룹 생성
```sql
SELECT 	DEPT_ID AS 부서,
		ROUND(AVG(SALARY),-4) AS 평균급여
FROM EMPLOYEE
GROUP BY DEPT_ID
ORDER BY 1;
```

### HAVING

- GROUP BY에 의해 그룹화된 데이터에 대한 그룹 함수의 실행 결과를 제한하기 위해 사용

```sql
SELECT DEPT_ID, SUM(SALARY)
FROM EMPLOYEE
GROUP BY DEPT_ID
HAVING SUM(SALARY) > 9000000;
```

### JOIN

- 서로 연관되고 다른 테이블에 존재하는 컬럼들을 한번에 조회하기 위해 사용하는 대표적인 기법

**오라클 전용 구문**

```sql
SELECT EMP_NAME, DEPT_NAME
FROM EMPLOYEE E, DEPARTMENT D
WHERE E.DEPT_ID = D.DEPT_ID;
```
**ANSI 표준 구문**

- `JOIN USING` : 조인 조건으로 사용하는 컬럼 이름이 동일한 경우 사용

```sql
SELECT EMP_NAME, DEPT_NAME
FROM EMPLOYEE
JOIN DEPARTMENT USING(DEPT_ID);
```

- `JOIN ON` : 조인 조건으로 사용하는 컬럼 이름이 서로 다른 경우 사용

```sql
SELECT DEPT_NAME, LOC_DESCRIBE
FROM DEPARTMENT
JOIN LOCATION ON (LOC_ID = LOCATION_ID);
```

#### OUTER JOIN

- 조건을 만족시키지 못하는 행까지 결과에 포함시키는 조인 유형

**오라클 전용 구문**

- 조인 조건을 만족시키는 행이 없는 테이블 기준 연산자 '+' 사용

```sql
SELECT EMP_NAME, DEPT_NAME
FROM EMPLOYEE E, DEPARTMENT D
WHERE E.DEPT_ID = D.DEPT_ID(+);
```

**ANSI 표준 구문**

- 전체 행을 모두 포함시켜야 하는 테이블 기준 `LEFT`, `RIGHT` 키워드 사용

```sql
-- 아래 쿼리의 결과는 위 쿼리의 결과와 같음
SELECT EMP_NAME, DEPT_NAME
FROM EMPLOYEE
LEFT JOIN department USING(DEPT_ID)
ORDER BY 2;
```

#### FULL OUTER JOIN

- 양쪽 테이블을 동시에 OUTER JOIN하는 ANSI 표준 구문(오라클 전용 구문은 지원되지 않음)

```sql
SELECT EMP_NAME, DEPT_NAME
FROM EMPLOYEE
FULL JOIN DEPARTMENT USING(DEPT_ID);
```

#### CROSS JOIN

- 대상 테이블의 모든 행에 대해 가능한 모든 조합을 생성하는 ANSI 표준 구문
- 오라클 구문에서는 조인 조건이 누락된 경우를 의미

```sql
SELECT *
FROM COUNTRY
CROSS JOIN LOCATION;
```

#### NON EQUIJOIN

```sql
SELECT EMP_NAME, SALARY, SLEVEL
FROM EMPLOYEE
JOIN SAL_GRADE ON (SALARY BETWEEN LOWEST AND HIGHEST)
ORDER BY 2 DESC;
```

#### SELF JOIN

- 한 테이블을 두 번 조인하는 유형
- 테이블 별칭을 사용해야 함

```sql
SELECT  E.EMP_NAME AS 직원,
        M.EMP_NAME AS 관리자
FROM EMPLOYEE E
JOIN EMPLOYEE M ON (E.MGR_ID = M.EMP_ID)
ORDER BY 1;
```

#### N개 테이블 JOIN

```sql
SELECT  EMP_NAME,
        JOB_TITLE,
        DEPT_NAME
FROM EMPLOYEE
JOIN JOB USING(JOB_ID)
JOIN DEPARTMENT USING(DEPT_ID);
```

### SET 연산자

- 두 개 이상의 쿼리 결과를 하나로 결합시키는 연산자

**유형**

- `UNION` : 양쪽 쿼리의 합집합 (중복 결과는 1번만 표현)
- `UNION ALL` : 양쪽 쿼리의 합집합 (중복 결과도 모두 표현)
- `INTERSECT` : 양쪽 쿼리의 교집합
- `MINUS` : 앞 쿼리-뒤 쿼리

```sql
SELECT EMP_ID, ROLE_NAME
FROM EMPLOYEE_ROLE
UNION
SELECT EMP_ID, ROLE_NAME
FROM ROLE_HISTORY;
```

### Subquery

- 하나의 쿼리가 다른 쿼리에 포함되는 구조

```sql
SELECT ...
FROM ...
WHERE expr operator ( 	SELECT ...
						FROM ...
						WHERE... );
```

#### 단일 행 서브쿼리

```sql
SELECT  EMP_NAME,
        JOB_ID,
        SALARY
FROM EMPLOYEE
WHERE SALARY = (SELECT MIN(SALARY)
                FROM EMPLOYEE);
```

#### 다중 행 서브쿼리

##### IN/NOT IN 연산자

```sql
SELECT  EMP_ID,
        EMP_NAME,
        '관리자' AS 구분
FROM EMPLOYEE
WHERE EMP_ID IN (SELECT MGR_ID FROM EMPLOYEE)
UNION
SELECT  EMP_ID,
        EMP_NAME,
        '직원'
FROM EMPLOYEE
WHERE EMP_ID NOT IN (SELECT MGR_ID FROM EMPLOYEE
                    WHERE MGR_ID IS NOT NULL)
ORDER BY 3, 1;
```

##### ANY/ALL 연산자

- `ANY`
  - `< ANY` : 비교 대상 중 최댓값보다 작음
  - `> ANY` : 비교 대상 중 최솟값보다 큼
  - `= ANY` : `IN` 연산자와 동일
- `ALL`
  - `< ALL` : 비교 대상 중 최솟값보다 작음
  - `> ALL` : 비교 대상 중 최댓값보다 큼

```sql
SELECT  EMP_NAME,
        SALARY
FROM EMPLOYEE
JOIN JOB USING(JOB_ID)
WHERE JOB_TITLE = '대리'
AND SALARY > ALL (  SELECT SALARY
                    FROM EMPLOYEE
                    JOIN JOB USING(JOB_ID)
                    WHERE JOB_TITLE = '과장');
```

##### 상관관계 서브쿼리

- 메인 쿼리에서 고려된 각 후보 행들에 대해 서브쿼리가 다른 결과를 반환해야 하는 경우에 유용

```sql
SELECT  EMP_NAME,
        JOB_TITLE,
        SALARY
FROM EMPLOYEE E
LEFT JOIN JOB J ON (E.JOB_ID = J.JOB_ID)
WHERE SALARY = (SELECT TRUNC(AVG(SALARY), -5)
                FROM EMPLOYEE
                WHERE NVL(JOB_ID, ' ') = 
                    NVL(E.JOB_ID, ' '))
ORDER BY E.JOB_ID;
```

##### EXISTS/NOT EXISTS 연산자

- 결과에 포함되는지의 여부를 확인해야 하는 경우에 유용한 연산자
- 존재 여부에 따라 TRUE 값을 반환

```sql
SELECT  EMP_ID,
        EMP_NAME,
        '관리자' AS 구분
FROM EMPLOYEE E
WHERE EXISTS (  SELECT NULL
                FROM EMPLOYEE
                WHERE E.EMP_ID = MGR_ID)
UNION
SELECT  EMP_ID,
        EMP_NAME,
        '직원'
FROM EMPLOYEE E2
WHERE NOT EXISTS (  SELECT NULL
                    FROM EMPLOYEE
                    WHERE E2.EMP_ID = MGR_ID)
ORDER BY 3, 1;
```

