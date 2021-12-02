## DDL

> Data Define Language : 데이터 정의 언어

#### CREATE TABLE : 테이블 생성

```sql
CREATE TABLE TABLE_NAME(
    COLUMN_NAME1 DATETYPE1 [DEFAULT EXPR1][CONSTRAINT1],
    COLUMN_NAME2 DATETYPE2 [DEFAULT EXPR2][CONSTRAINT2],
    COLUMN_NAME3 DATETYPE3 [DEFAULT EXPR3][CONSTRAINT3],
    ...
    TABLE_CONSTRAINT
);
```

**예시**

```sql
CREATE TABLE TEST_MEMBER(
    ID VARCHAR2(50) PRIMARY KEY,
    PWD VARCHAR2(50),
    ADDR VARCHAR2(50)
);
```

##### 제약조건

- `NOT NULL` : 컬럼 값이 NULL이 될 수 없도록 함
- `UNIQUE` : 컬럼 내의 모든 값이 하나씩만 존재하도록 함
- `DEFAULT` : 값을 설정하지 않을 시 자동으로 설정할 값을 설정
- `CHECK 조건식` : 조건식에 맞는 데이터만 저장하도록 함 
- `PRIMARY KEY` : 해당 컬럼을 기본키로 설정
- `FOREIGN KEY` : 해당 컬럼을 외래키로 설정
  - 외래키(FOREIGN KEY) : 부모에 의존하는 데이터

**예시**

```sql
CREATE TABLE TEST_MEMBER(
    ID VARCHAR2(50),
    PWD VARCHAR2(50) NOT NULL,		/* 컬럼 레벨 제약조건 설정 */ 
    ADDR VARCHAR2(50) DEFAULT 'SEOUL',
    PRIMARY KEY(ID)		/* 테이블 레벨 제약조건 설정 */ 
);
```

```sql
CREATE TABLE TEST_FK(
    ID CHAR(3) PRIMARY KEY,
    NAME VARCHAR(50) NOT NULL,
    LID CHAR(2),
    FOREIGN KEY(LID) REFERENCES LOCATION(LOCATION_ID)
);
```

```sql
CREATE TABLE TEST_COMPOSIT_PK(
    ID  VARCHAR2(50) UNIQUE,
    NAME VARCHAR2(50),
    SALARY NUMBER CHECK (SALARY > 0),
    GENDER CHAR(1) CHECK (GENDER IN ('M', 'F')),
    PRIMARY KEY (ID, NAME)
); 
```

#### DROP : 테이블 삭제

```sql
DROP TABLE TABLE_NAME;
```



## DML - INSERT, UPDATE, DELETE

#### INSERT : 데이터 삽입

`INSERT INTO TABLE NAME([컬럼리스트]) VALUES(VALUE, VALUE...);`

**예시**

```sql
INSERT INTO TEST_MEMBER(ID, PWD, ADDR) VALUES('JSLIM', 'JSLIM', 'GWANGJU');
INSERT INTO TEST_MEMBER VALUES('JYU', 'JYU', 'SEOUL');
INSERT INTO TEST_MEMBER(ID, PWD) VALUES('WOOK', 'WOOK');
INSERT INTO TEST_MEMBER VALUES('DAVID', NULL, NULL);
```

#### UPDATE : 데이터 변경

```SQL
UPDATE TABLE_NAME
SET COLUMN_NAME1 = VALUE1, COLUMN_NAME2 = VALUE2...
WHERE CONDITIONS;
```

**예시**

```sql
UPDATE TEST_DML
SET MARRIAGE = 'Y', SALARY = 200
WHERE ID = 'JSLIM';
```

#### DELETE : 데이터 삭제

```sql
DELETE
FROM TABLE_NAME
WHERE CONDITIONS;
```

**예시**

```sql
DELETE
FROM TEST_DML
WHERE ID = 'ADMIN';
```
