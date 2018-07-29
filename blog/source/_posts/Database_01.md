---
title: Database 개념 및 기초
date: 2018-07-25 21:33:48
tags: Database
categories: Database
---

# Database 개념 및 기초

## 1. Database 개요

### 1.1 데이터베이스의 개념

DB(Database)
- 방대한 데이터를 효율적으로 관리하기 위해 컴퓨터에 통합·저장한 것
- 통합하여 관리되는 데이터들의 집합

DBMS(Database Management System)
- 데이터베이스를 관리하는 미들웨어 시스템
- 데이터베이스에 데이터를 저장하고, 효율적으로 검색하고 수정할 수 있는 환경을 제공
- 권한이 없는 사용자가 접근하거나 시스템에 장애가 생겼을 때에도 데이터를 안전하게 보호하며, 여러 사용자가 데이터베이스에 동시에 접근할 수 있도록 제어
- 대표적인 DBMS: Oracle, MySQL 등

 
### 1.2 데이터베이스의 특징
- 한 조직의 여러 응용 프로그램이 저장된 데이터를 공유할 수 있도록 데이터를 통합하여 관리

- 데이터베이스에 저장된 데이터의 특징
	- 통합되어 저장됨
	- 물리적인 기억장치에 보관됨
	- 필요에 따라 삽입, 삭제, 변경됨
	- 여러 사람이 사용함

- 데이터베이스의 특징
	- 실시간으로 접근 가능
	- 계속 변화함
	- 동시 공유가 가능
	- 내용에 따라 참조


### 1.3 데이터베이스 언어

1. 데이터 정의어(DDL, Data Definition Language)
	- 데이터 저장 구조, 데이터 접근 방법, 데이터 형식 등 데이터베이스를 구축하거나 수정할 때 사용하는 언어

2. 데이터 조직어(DML, Data Manipulation Language)
	- 데이터 베이스에 저장된 데이터를 검색, 수정, 삽입, 삭제할 때 사용하는 언어로, 사용자와 DBMS 사이의 인터페이스를 제공
	- 대표적 데이터 조직어: query
	- 절차적언어 & 비절차적 언어로 구분
		- 절차적 언어(procedural language): 필요한 데이터와 검색 방법까지 명시
		- 비절차적 언어(non-procedural language): 필요한 데이터만 명시하고 검색 방법은 명시하지 않음
			- SQL이 대표적 비절차적 언어  

3. 데이터 제어어(DCL, Data Control Language)
	- 데이터를 보호하고 관리할 때 사용하는 언어
	- 데이터의 무결성 유지, 보안 및 접근 제어, 시스템 장애로부터의 복구, 병행 수행 제어 기능 등을 담당 


### 1.4 데이터베이스 사용자
DBMS 활용 형태에 따라 세 가지 유형으로 구분
- 응용프로그래머
	- 일반 프로그래밍언어와 데이터조작어를 이용하여 프로그램을 만듦
 
- 최종 사용자
	- 데이터의 검색, 삽입, 삭제, 갱신 등을 위해 DBMS를 사용하는 사람
	- 데이터베이스 질의어를 사요아여 데이터베이스 시스템에 접근한 후 원하는 정보를 찾음   

- 데이터베이스 관리자
	- 데이터 정의어와 데이터 제어어를 사용하여 데이터베이스 스키마를 생성하고 관리
	- 주요 업무: 데이터베이스 스키마의 생성과 변경, 무결성 제약 조건 명시, 보안 정책 수립(사용자의 권한 설정 및 역할 관리), 저장 구조 및 접근 방법 정의, 백업과 복구 절차 수립, 표준화 시행 등 
  
### 1.5 데이터베이스의 구분

1. 관계형 데이터베이스(RDBMS, Relational Database Management System)
	- 관계형 데이터 모델을 기반으로 하며 가장 널리 사용되는 데이터베이스
	- Oracle, **MySQL**, Postgresql, Sqlite 등
	- 데이터 테이블 사이에 키값으로 관계를 가지고 있는 데이터베이스
	- 데이터 사이의 관계 설정으로 최적화된 스키마를 설계 가능

2. NoSQL
	- **Mongodb**, Hvase, Cassandra 등
	- 데이터 테이블 사이에 관계가 없이 저장하는 데이터베이스
	- 데이터 사이의 관계가 없으므로 복잡성이 줄고 많은 데이터를 저장가능하고 데이터 수정도 용이
	- RDBMS와 달리 data가 중복되어 저장되므로 row수가 늘어나지만 insert 속도가 빨라 big data 처리와 관련해 최근 주목 받게 됨	


## 2. RDBMS(관계형 데이터베이스)

### 2.1 RDBMS의 개요
특징
- 구조가 단순하고 데이터 분류, 정렬, 탐색속도가 빠름
- 오래 사용된 만큼 신뢰성이 높음
- 스키마 수정이 어려움  

구조
- Server > Database > Table > Row > Value

### 2.2 RDBMS의 구조
1. Table
	- row와 column으로 이루어진 데이터베이스를 구성하는 기본 단위
	- python pandas의 DataFrame에 해당
	- Storage Engine
		- 어떤 data를 쓸지에 따라 결정 (보통 InnoDB 많이 사용)
		1. MyISAM: full text index 지원, table 단위 lock(단점), select가 빠름, 구조 단순
		2. InnoDB: transaction 지원, row 단위 lock(장점), 자원을 만이 사용, 구조 복잡 

2. Row
	- 테이블의 각 행, tuple 또는 record라고도 함
	- cardinality: row(tuple)의 개수

3. Column
	- 데이터의 각 열, field 또는 attribute라고도 함
	- degree(차수): tuple을 구성하는 attribute의 개수 (column수)
	- domain: attirube 하나가 가질 수 있는 **값**의 집합

4. Value
	- row와 column에 포함되어 있는 데이터

5. Key
	- row에서 unique한 값으로, row의 식별자로 사용
	- key의 종류
		1. 후보키(candidate key):
			- 각 row를 구별할 수 있는 최소한의 속성으로 구성된 키
			- 두 개 column의 조합이 후보 키가 될 수도 있음 (이 경우 어떤 한 속성을 제거하면 구별 능력을 상실)
		2. 기본키(primary key): 후보키 중 대표로 선정한 key 
		3. 대체키(alternate key): 기본키가 아닌 후보키
		4. 외래키(foreign key): 다른 테이블의 기본키를 참조하며, 테이블 사이의 관계를 나타내는 키

6. Relation
	- 두 개의 table은 일대일(1:1, one-to-one), 일대다(1:n, one-to-many), 다대다(n:n, many-to-many)의 관계를 가질 수 있음


### 2.3 Schema
1. Schema
	- Schema: 데이터베이스의 구조에 대한 디자인

2. 무결성 제약 조건(integrity constraint)
	- 데이터베이스 상태가 만족해야 하는 조건으로, 사용자가 데이터베이스를 갱신할 때 데이터베이스의 일관성을 손상하지 않도록 보장하는 수단
	- schema를 정의할 때 한 번만 명시하면 데이터베이스가 갱신될 때 DBMS가 자동으로 검사
	- 무결성 제약조건의 구분
		- 도메인 무결성 제약 조건
			- 각 속성값은 반드시 도메인에 속한 값을 가져야 함
			- 속성의 default, 가능한 값의 범위, null값 허용 여부 등을 지정
		- 개체 무결성 제약 조건
			- 기본키를 구성하는 속성은 null값을 가질 수 없음
		- 참조 무결성 제약 조건
			- 외래키 값은 참조된 테이블의 기본키와 도메인이 동일해야 함 
	

## 3. NoSQL

### 3.1 NoSQL의 개요
NoSQL의 개념
- NoSQL: Not Only SQL
- RDBMS의 한계(확장성이 낮음)를 극복하기 위해 만들어진 데이터베이스

NoSQL의 특징
- 확장성이 좋음 → 데이터의 분산처리 용이
- 데이터 저장이 유연: RDBMS와 다르게 구조의 변경이 불필요
- Schema 및 join이 없음
- collection 별로 관계가 없이 때문에 모든 데이터가 들어있어야 함
- 저장되는 데이터는 key-value 형태의 JSON 포맷 사용
- select는 RDBMS보다 느리지만 Insert는 빨라 대용량 데이터베이스에 많이 사용됨
- Transaction이 지원되지 않음(동시수정에 대한 신뢰성이 지원되지 않음)
	- 금융권 같은 곳에서는 사용할 수 없음

### 3.2 Mongodb
Mongodb
- C++로 작성된 오픈소스 데이터 베이스
- 뛰어난 확장성과 성능을 가짐
- NoSQL에서는 인지도가 가장 높음

Mongodb의 구조
- Server > Database > Collection > Document > key:value
- Collection: RDBMS의 Table과 같은 개념
- Document: RDBMS의 Row와 같은 개념
- Key: RDBMS의 Column과 같은 개념
  
  
  
----    
#### ※ 참고 자료
- 패스트캠퍼스 '데이터 사이언스 스쿨 Python 8기' 수업자료
- 이동명, 권오현, 고정국, 「컴퓨터 사이언스 개정판」
