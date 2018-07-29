---
title: MySQL 
date: 2018-07-25 22:13:26
tags: 
- Database
- MySQL
- SQL
categories: Database
---

# MySQL

## 1. SQL 소개
SQL(Structured Query Language)
- 관계형 데이터베이스를 조작하고 관리할 때 사용하는 데이터베이스 질의용 언어
- 1970년대 IBM에서 개발하여 IBM의 관계형 DBMS에 처음으로 사용
- 1986년 미국표준협회(ANSI)가 SQL 표준으로 채택하면서 현재까지 다양한 DBMS의 구조화 질의어로 널리 사용되고 있음
- 비절차적 언어이기 때문에 절차적언어에 비해 배우기 쉬움
- 자연어에 가까운 구문을 사용해 query를 표현하며 관계형 대수나 관계형 해석에 비해 표현력이 우수함

SQL의 기능
1. 데이터 정의 기능
	- 데이터 정의어(DDL)를 이용하여 테이블 생성 및 제거, 속성의 추가 및 삭제, view의 생성 및 제거, index의 생성 및 제거 등의 작업 수행
	- 테이블을 생성하면서 여러 가지 무결성 제약 조건 기술
2. 데이터 조작 기능
	- 데이터 조작어(DML)를 이용하여 데이터의 검색, 삽입, 삭제, 수정 등의 연산을 수행
3. 데이터 제어 기능
	- 데이터 제어어(DCL)를 이용하여 transaction의 시작, 철회, 완료 등을 명시하고 table에 대해 권한을 부여하거나 취소


## 2. MySQL Basic Command
MySQL shell을 이용한 기본 명령

### 1) Dabatase

- DB 목록 보기
```sql 
mysql> show databases;
```

- DB 만들기
```sql 
mysql> create databases db_name;
```

- DB 접속
```sql 
mysql> use databases db_name;
```
- 현재 접속 중인 DB 확인
```sql 
mysql> select database();

```

- DB 삭제
```sql 
mysql> drop databases db_name;
```

### 2) Table
- Table 만들기
```sql 
-- name(문자열 20자), age (숫자 3자) column이 있는 user 테이블 생성 
mysql> create table user(name char(20), age int(3));
```

- Table 목록 확인 
	- 테이블 추가나 삭제 후 table 목록 확인
```sql 
mysql> show tables;
```

- Table 구조 확인
```sql 
-- table name: user
mysql> desc table user;
mysql> describe table user;
mysql> explain table user;
```

- Table 이름 바꾸기
```sql 
-- user에서 user1로 이름 변경
mysql> rename table user to user1;
```

- Table에 데이터 추가
```sql 
mysql> insert into user1(name, age) values("alice", 23);
mysql> insert into user1(name, age) values("peter", 30);
```

- 추가된 데이터 확인
```sql 
mysql> select * from user1;
```

- Table 삭제
```sql 
mysql> drop table user1;
```

----    
#### ※ 참고 자료
- 패스트캠퍼스 '데이터 사이언스 스쿨 Python 8기' 수업자료
- 이동명, 권오현, 고정국, 「컴퓨터 사이언스 개정판」
