---
title: MySQL Basic Syntax
date: 2018-07-26 00:48:26
tags: 
- Database
- MySQL
- SQL
categories: Database
---

# MySQL Basic Syntax
본격적으로 RDBMS(나의 경우는 workbench)를 사용하여 MySQL 문법을 익혀보자
- 명령어는 대문자로 쓰는 것이 컨벤션이나 소문자로 써도 실행에는 문제가 없음
- 마지막에 세미콜론(;) 또한 쓰지 않아도 실행에는 문제가 없음

## 1. Create
### 1) Database
- Database 생성
```sql
CREATE DATABASE <db_name>;
```
- Database 선택
```sql
USE <db_name>;
```
- 현재 database 확인
```sql
SELECT DATABASE();
```

### 2) Table
- Table을 생성할 때에는 컬럼이름, 데이터타입, 제약조건에 대한 내용이 들어감
- Table 생성
```sql
CREATE TABLE <table_name>(
	column_name_1 column_datatype_1 column_constraint_1,
    column_name_2 column_datatype_2 column_constraint_2,
    ...
)
```
- 제약조건이 없는 user1 Table 생성
```sql
CREATE TABLE user1(
	user_id INT,
    name Varchar(20),
    email Varchar(30),
    age INT(3),
    rdate DATE
)
```
- 제약조건이 있는 user2 Table 생성
```sql
CREATE TABLE user2(
	user_id INT PRIMARY KEY AUTO_INCREMENT,
    name Varchar(20) NOT NULL,
    email Varchar(30) UNIQUE NOT NULL,
    age INT(3) DEFAULT '30',
    rdate TIMESTAMP
)
```
- Database 선택
```USE <db_name>;```
- 현재 database 확인
```SELECT DATABASE();```

## 2. Alter
### 1) Database: encoding 변경
- 현재 문자열 인코딩 확인
```sql
show variables like "character_set_database";
```
- test 데이터베이스의 문자열 인코딩을 utf8로 변경
```sql
ALTER DATABASE test CHARACTER SET = utf8;
ALTER DATABASE test CHARACTER SET = ascii;
```
- 문자열 encoding 변경 결과 확인
```sql
show variables like "character_set_database";
```

### 2) Table: column 추가, 삭제, 수정
- ADD
```sql 
-- user2 테이블에 TEXT 데이터 타입을 갖는 tmp column 추가
ALTER TABLE user2 ADD tmp TEXT;
```
- MODIFY
```sql 
-- user2 테이블에 tmp column을 INT(3) 데이터 타입으로 수정
ALTER TABLE user2 MODIFY COLUMN tmp INT(3);
```
- DROP
```sql 
-- user2 테이블의 tmp column을 삭제
ALTER TABLE user2 DROP tmp;
```

## 3. DROP
### 1) Database
- Database 삭제
```sql
DROP DATABASE <db_name>;
```

### 2) Table
- Table 삭제
```sql
DROP TABLE <table_name>;
```

## 4. INSERT
### 1) Syntax
- Table 뒤에 오는 column이름은 삭제 가능, 대신 VALUES 뒤에 value값이 순서대로 와야 함
```sql
INSERT INTO <table_name>(<column_name_1>, <column_name_1>, ...)
VALUES(<value_1>, <value_2> ...)
```
- 여러 row를 한번에 insert하기
```sql
INSERT INTO <table_name>(<column_name_1>, <column_name_1>, ...)
VALUES(<value_1>, <value_2> ...),
(<value_1>, <value_2> ...),
...
(<value_1>, <value_2> ...);
```

### 2) example
- user1 테이블에 user_id, name, email, age, rdate를 입력
```sql
INSERT INTO user1(user_id, name, email, age, rdate)
VALUES(1, "jane", "jane@gmail.com", 30, now()),
(2, "peter", "peter@gmail.com", 33, '2017-02-20'),
(3, "alice", "alice@gmail.com", 23, '2018-01-15'),
(4, "po", "po@gmail.com", 43, '2002-09-16'),
(5, "andy", "andy@gmail.com", 17, '2016-04-28'),
(6, "jane", "jane1234@gmail.com", 33, '2013-09-02');
```








----    
#### ※ 참고 자료
- 패스트캠퍼스 '데이터 사이언스 스쿨 Python 8기' 수업자료
- 이동명, 권오현, 고정국, 「컴퓨터 사이언스 개정판」
