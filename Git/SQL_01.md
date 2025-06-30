# 250630

### **MySQL 설치, DDL, CRUD, 주요 제약조건(UNIQUE, DEFAULT)**

# 내정리

## ✅ DDL이란?

> DDL (Data Definition Language)
> 
> 
> : 데이터베이스의 구조(스키마)를 정의하거나 변경할 때 사용하는 **SQL 명령어 집합**
>   데이터 자체가 아니라 **데이터를 담는 구조를 다룸**
> 

즉, **테이블, 데이터베이스, 컬럼, 제약조건 등을 생성·수정·삭제**할 때 사용하는 명령들이야.

---

## ✅ DDL의 대표 명령어들

| 명령어 | 설명 |
| --- | --- |
| `CREATE` | 테이블, 데이터베이스, 뷰 등을 **새로 생성** |
| `ALTER` | 기존 테이블 등의 구조를 **수정** (컬럼 추가, 변경 등) |
| `DROP` | 테이블 또는 데이터베이스를 **삭제** |
| `TRUNCATE` | 테이블의 **모든 데이터를 삭제** (구조는 유지) |
| `RENAME` | 테이블이나 컬럼 이름을 **변경** |

### ✅ 예제

### 🔹 `CREATE`

```sql
CREATE TABLE users (
  id INT PRIMARY KEY,
  name VARCHAR(50)
);
```

### 🔹 `ALTER`

```sql
ALTER TABLE users ADD age INT;
```

### 🔹 `DROP`

```sql
DROP TABLE users;
```

### 🔹 `TRUNCATE`

```sql
TRUNCATE TABLE users;
```

### 🔹 `RENAME`

```sql
RENAME TABLE users TO members;
```

---

## ✅ 3. DDL (데이터 정의어)

### 3.1 데이터베이스 생성

```sql
CREATE DATABASE testdb;
USE testdb;

```

### 3.2 테이블 생성

```sql
CREATE TABLE users (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  age INT DEFAULT 20,
  email VARCHAR(100) UNIQUE
);
```

> ✅ 여기서 DEFAULT와 UNIQUE가 제약조건임
> 

---

## ✅ CRUD 예시 (DML)

### 🔹 Create (삽입)

```sql
INSERT INTO users (name, email) VALUES ('Kim', 'kim@example.com');
```

### 🔹 Read (조회)

```sql
SELECT * FROM users;
```

### 🔹 Update (수정)

```sql
UPDATE users SET age = 30 WHERE name = 'Kim';
```

### 🔹 Delete (삭제)

```sql
DELETE FROM users WHERE name = 'Kim';
```

---

## ✅ 주요 제약조건 요약

| 제약조건 | 설명 | 예시 |
| --- | --- | --- |
| `PRIMARY KEY` | 기본키, 중복/NULL 불가 | `id INT PRIMARY KEY` |
| `AUTO_INCREMENT` | 자동 번호 증가 | `id INT AUTO_INCREMENT` |
| `NOT NULL` | NULL 금지 | `name VARCHAR(100) NOT NULL` |
| `UNIQUE` | 유일한 값만 허용 | `email VARCHAR(100) UNIQUE` |
| `DEFAULT` | 기본값 설정 | `age INT DEFAULT 20` |
| `CHECK` | 조건 만족시만 허용 | `CHECK (age >= 0)` *(MySQL 8 이상)* |
| `FOREIGN KEY` | 외래키 제약조건 | `FOREIGN KEY (col) REFERENCES other_table(id)` |

---

## ✅ **데이터베이스, 테이블, 컬럼 정의**

## 1. 데이터베이스(Database)

### 🔹 정의:

- 데이터를 체계적으로 **보관하는 저장소** (전체 그릇)
- 여러 개의 테이블을 포함할 수 있는 **최상위 단위**

### 🔹 특징:

- 하나의 데이터베이스 안에는 **여러 테이블**이 존재할 수 있음
- 실제 파일 형태로 디스크에 저장됨
- `USE 데이터베이스명;` 명령으로 활성화

### 🔹 예시:

```sql
CREATE DATABASE school;

```

---

## 2. 테이블(Table)

### 🔹 정의:

- 데이터베이스 안에 존재하는 **데이터 저장 단위**
- 행(row)과 열(column)로 구성된 구조

### 🔹 특징:

- 각각의 행 = 하나의 **레코드(record)** (데이터 한 줄)
- 각각의 열 = 하나의 **컬럼(column)** (속성/필드)
- **동일한 구조의 데이터들**을 모아놓은 곳

### 🔹 예시:

```sql
CREATE TABLE students (
  id INT,
  name VARCHAR(50),
  age INT
);

```

---

## 3. 컬럼(Column)

### 🔹 정의:

- 테이블 안의 **열(속성)**
- 각각의 컬럼은 특정 **데이터 타입**을 가짐 (숫자, 문자, 날짜 등)

### 🔹 특징:

- 컬럼 이름은 해당 속성을 의미 (ex. 이름, 나이, 등록일 등)
- 각 컬럼은 **제약조건**을 가질 수 있음 (`NOT NULL`, `UNIQUE`, 등)
- 한 컬럼은 **모든 행에서 동일한 타입의 값**을 가짐

### 🔹 예시:

```sql
name VARCHAR(50) NOT NULL

```

---

## 차이점 요약 표

| 구분 | 설명 | 포함 관계 | 예시 |
| --- | --- | --- | --- |
| **데이터베이스** | 데이터의 전체 저장소 | 테이블들을 포함 | `school` |
| **테이블** | 데이터가 저장되는 구조화된 공간 | 컬럼과 행 포함 | `students` |
| **컬럼** | 테이블의 열, 속성 정의 | 테이블의 구성 요소 | `name`, `age` |

---

## 비유로 설명

| 용어 | 비유 |
| --- | --- |
| 데이터베이스 | 엑셀 파일 전체 |
| 테이블 | 엑셀 시트 한 장 |
| 컬럼 | 엑셀 시트의 열 (A열, B열...) |
| 행(Row) | 한 줄의 데이터 (한 사람의 정보 등) |

---

## 전체 구조 예시

```sql
-- 1. 데이터베이스 생성
CREATE DATABASE mydb;

-- 2. 사용
USE mydb;

-- 3. 테이블 생성
CREATE TABLE employees (
  emp_id INT PRIMARY KEY,
  name VARCHAR(50),
  hire_date DATE
);

```

---

필요하면, 행(Row), 레코드(Record) 등 다른 용어들도 정리해줄게!

# 강사님정리

### **📊 데이터베이스 핵심 개념**

### **데이터 베이스의 종류**

- **RDBMS ← 가장 널리 많이 쓰임**
    - MySQL
    - PostgreSQL
    - Oracle
    - SQlite
    - Maria DB
    - …
- Document DB (A.K.A NoSQL)
- Key-Value DB
- Graph DB
- …

### **스키마(Schema)**

- **정의**: 데이터베이스의 구조와 제약조건을 정의한 것
- **포함 요소**: 테이블 구조, 데이터 타입, 제약조건, 관계 등
- **역할**: 데이터가 어떻게 저장되고 관리될지 설계도 역할

### **DDL vs DML**

| 구분 | DDL (Data Definition Language) | DML (Data Manipulation Language) |
| --- | --- | --- |
| **목적** | 데이터베이스 구조 정의/변경 | 데이터 조작 |
| **대상** | 테이블, 데이터베이스, 스키마 | 데이터 (행) ⇒ record |
| **주요 명령어** | `CREATE`, `ALTER`, `DROP`,`TRUNCATE` | `INSERT`, `SELECT`, `UPDATE`, `DELETE` |
| **실행 결과** | 구조 변경 | 데이터 변경 |

---

### **🗄️ 데이터베이스 관리 (DDL)**

```sql

-- 데이터베이스 생성
CREATE DATABASE database_name;

-- 데이터베이스 선택
USE database_name;

-- 데이터베이스 목록 조회
SHOW DATABASES;

-- 데이터베이스 삭제
DROP DATABASE IF EXISTS database_name;

```

---

### **📋 테이블 관리 (DDL)**

### **테이블 생성**

```sql

CREATE TABLE table_name (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(30) NOT NULL,
  email VARCHAR(50) UNIQUE,
  created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);

```

### **테이블 구조 확인**

```sql

-- 테이블 목록
SHOW TABLES;

-- 테이블 구조
DESC table_name;

```

### **테이블 구조 변경**

```sql

-- 컬럼 추가
ALTER TABLE table_name ADD COLUMN column_name datatype;

-- 컬럼 이름 + 데이터 타입 수정
ALTER TABLE members CHANGE COLUMN column_name new_name datatype;

-- 컬럼 데이터 타입 수정
ALTER TABLE members MODIFY COLUMN column_name datatype;

-- 컬럼 삭제
ALTER TABLE table_name DROP COLUMN column_name;

```

### **테이블 삭제**

```sql

DROP TABLE IF EXISTS table_name;

```

---

### **📝 데이터 조작 (DML)**

### **INSERT - 데이터 입력**

```sql

-- 단일 행 입력
INSERT INTO table_name (column1, column2) VALUES (value1, value2);

-- 다중 행 입력
INSERT INTO table_name (column1, column2) VALUES
(value1, value2),
(value3, value4);

```

### **SELECT - 데이터 조회**

```sql

-- 전체 조회
SELECT * FROM table_name;

-- 특정 컬럼 조회
SELECT column1, column2 FROM table_name;

-- 조건부 조회
SELECT * FROM table_name WHERE condition;

```

### **UPDATE - 데이터 수정**

```sql

UPDATE table_name SET column1 = value1 WHERE condition;

```

### **DELETE - 데이터 삭제**

```sql

DELETE FROM table_name WHERE condition;

```

---

### **🔐 주요 제약조건**

### **PRIMARY KEY**

- **목적**: 각 행의 고유 식별자
- **특징**: 중복 불가, NULL 불가, 테이블당 1개

```sql

id INT AUTO_INCREMENT PRIMARY KEY

```

### **NOT NULL**

- **목적**: 필수 입력 강제
- **특징**: 빈 값 입력 불가

```sql

name VARCHAR(30) NOT NULL

```

### **UNIQUE**

- **목적**: 중복 값 방지
- **특징**: 중복 불가, NULL 허용, 여러 개 가능

```sql

email VARCHAR(50) UNIQUE

```

### **DEFAULT**

- **목적**: 기본값 자동 입력
- **특징**: 값 미입력 시 기본값 사용

```sql

CREATE TABLE new_table (
	status VARCHAR(10) DEFAULT 'active',
	join_date DATE DEFAULT(CURRENT_DATE)
);

```

### **AUTO_INCREMENT**

- **목적**: 숫자 자동 증가
- **특징**: 주로 PRIMARY KEY와 함께 사용

```sql

id INT AUTO_INCREMENT PRIMARY KEY

```

---

### **📊 주요 데이터 타입**

| 타입 | 설명 | 예시 |
| --- | --- | --- |
| `INT` | 정수 | `age INT` |
| `VARCHAR(n)` | 가변 문자열 | `name VARCHAR(50)` |
| `TEXT` | 긴 문자열 | `content TEXT` |
| `DATE` | 날짜 | `birth_date DATE` |
| `DATETIME` | 날짜+시간 | `created_at DATETIME` |

---

### **⚠️ 주의사항**

### **안전한 쿼리 작성**

```sql

-- ❌ 위험 (모든 데이터 영향)
UPDATE users SET status = 'inactive';
DELETE FROM users;

-- ✅ 안전 (조건 지정)
UPDATE users SET status = 'inactive' WHERE id = 1;
DELETE FROM users WHERE status = 'deleted';

```

### **WHERE 절 필수 상황**

- `UPDATE`: 특정 데이터만 수정
- `DELETE`: 특정 데이터만 삭제
- `SELECT`: 조건에 맞는 데이터만 조회

### **IF EXISTS 사용**

```sql

-- 에러 방지
DROP TABLE IF EXISTS table_name;
DROP DATABASE IF EXISTS database_name;

```

---

### **🎯 핵심 포인트**

1. **DDL**로 구조를 만들고, **DML**로 데이터를 다룬다
2. **스키마**는 데이터베이스의 설계도
3. **제약조건**은 데이터 무결성 보장
4. **WHERE 절**은 안전한 데이터 조작의 핵심
5. **PRIMARY KEY + AUTO_INCREMENT**는 기본 패턴
6. **DEFAULT + CURRENT_TIMESTAMP**로 자동 시간 입력