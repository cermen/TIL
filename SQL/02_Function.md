# SQL 함수

>하나의 큰 프로그램에서 반복적으로 사용되는 부분들을 분리한 작은 서브 프로그램

### 문자열 함수

#### LENGTH, LENGTHB

- `LENGTH` 함수 : 주어진 컬럼 값/문자열 길이(문자 개수)를 반환하는 함수
- `LENGTHB` 함수 : 주어진 컬럼 값/문자열 길이(Byte)를 반환하는 함수
- 구문 : `LENGTH[B](string)`

#### INSTR

- 찾는 문자(열)이 지정한 위치부터 지정한 횟수만큼 나타난 시작 위치를 반환하는 함수
- `INSTR(문자열, 찾을 문자(열), [position, [occurrence]])`

#### LPAD/RPAD

- 주어진 컬럼/문자열에 임의의 문자(열)을 왼쪽/오른쪽에 덧붙여 길이 N의 문자열을 반환하는 함수
- `LPAD(문자열, 반환할 문자 수, [str])`
- `RPAD(문자열, 반환할 문자 수, [str])`

#### LTRIM/RTRIM

- 주어진 컬럼/문자열에 임의의 문자(열)을 왼쪽/오른쪽에 덧붙여 길이 N의 문자열을 반환하는 함수
- `LTRIM(문자열, str)`
- `RTRIM(문자열, str)`

#### TRIM

- 주어진 컬럼/문자열의 앞/뒤/양쪽에 있는 지정한 문자를 제거한 나머지를 반환하는 함수
- `TRIM(문자열)`
- `TRIM(제거할 문자 FROM 문자열)`
- `TRIM(LEADING|TRAILING|BOTH [제거할 문자] FROM 문자열)`
  - LEADING|TRAILING|<u>BOTH</u> : 제거할 위치 지정(각각 앞/뒤/양쪽)

#### SUBSTR

- 주어진 컬럼/문자열에서 지정한 위치부터 지정한 개수 만큼의 문자열을 잘라내어 반환하는 함수
- `SUBSTR(문자열, 시작 위치, [길이])`

### 숫자 함수

#### ROUND

- 지정한 자릿수에서 반올림하는 함수
- `ROUND(숫자, [반올림할 소숫점 자릿수])`

#### TRUNC

- 지정한 자릿수에서 버림하는 함수
- `TRUNC(숫자, [버림할 소숫점 자릿수])`

### 날짜 함수

#### SYSDATE

- 지정된 형식으로 현재 날짜와 시간을 표시하는 함수
- 기본 설정 형식(한글 버전 기준) : 'YY/MM/DD'

#### ADD_MONTHS

- 지정한 만큼의 달 수를 더한 날짜를 반환하는 함수
- `ADD_MONTHS(기준 날짜, 더하려는 개월 수)`

#### MONTHS_BETWEEN

- 지정한 두 날짜 사이의 월 수를 반환하는 함수
- `MONTHS_BETWEEN(date1, date2)`
  - date1 > date2 : 양수 반환
  - date1 < date2 : 음수 반환

### 데이터 타입 변환 함수

#### TO_CHAR

- NUMBER/DATE 타입을 CHARACTER 타입으로 반환하는 함수
- `TO_CHAR(input_type[, format])`
  - format : 숫자/날짜 표현형식

#### TO_DATE

- CHARACTER 타입을 DATE 타입으로 반환하는 함수
- `TO_DATE(input_type[, format])`
  - format : input_type의 날짜 표현형식

##### RR 날짜 형식

* YY 날짜 형식과 유사
* 지정한 연도와 현대 연도에 따라 반환하는 세기 값이 달라짐

#### TO_NUMBER

- CHARACTER 타입을 NUMBER 타입으로 반환하는 함수
- `TO_NUMBER(input_type[, format])`

### 기타 함수

#### NVL

- NULL을 지정한 값으로 변환하는 함수
- 오라클 전용 함수
- `NVL(expr1, expr2)`
  - expr1 : NULL을 포함하는 컬럼
  - expr2 : expr1이 NULL인 경우 변환할 값

#### DECODE

- SELECT 구문으로 IF-ELSE 논리를 제한적으로 구현한 오라클 DBMS 전용 함수
- `DECODE(expr, search1, result1[, searchN, resultN,...][, default ])`
  - expr : 대상 컬럼 또는 문자(열)
  - search : expr과 비교하려는 값
  - result : expr = search 인 경우의 반환 값
  - default : expr != search 인 경우의 반환 값 (지정하지 않을 경우 NULL 반환)

#### CASE

- DECODE 함수와 유사한 ANSI 표준 구문
- `CASE 대상 컬럼/문자(열) WHEN search1 THEN result1 [WHEN..THEN..][ELSE default] END`
- `CASE WHEN condition1 THEN result1 [WHEN..THEN..][ELSE default] END` 

### 그룹 함수

- `SUM()` : 총합 계산
- `AVG()` : 평균 계산
- `MIN()`, `MAX()` : 최솟값/최댓값 반환
- `COUNT()` :결과값의 전체 행 수 변환

```sql
SELECT MIN(컬럼명)
FROM 테이블명
WHERE 조건;
```

