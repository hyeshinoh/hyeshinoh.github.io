## MySQL intermediate Syntax

### 1. 숫자 올림, 반올림, 내림
1. 올림
	- `ceil(숫자)`
	- 자릿수를 지정할 수 없기 때문에 아래와 같은 trick이 필요 
```sql
select ceil(12.345)
-- 올림 자릿수 지정
select ceil(12.345*10)*0.1
-- 올림 활용
use world
select percentage, ceil(percentage)
from countrylanguage
```
2. 반올림
 	- `round(숫자, 결과 소수점 자릿수)`
```
select round(12.345, 2)
select percentage, round(percentage,0)
from countrylanguage
```
3. 내림
	- `truncate(숫자, 결과 소수점 자릿수)`
	- 참고: truncate은 table을 삭제할 때도 사용하는데, delete table과 달리 truncate table은 아예 테이블을 초기화시킴
```
select truncate(12.345, 1)
select percentage, truncate(percentage,1)
from countrylanguage
```

### 2. 조건문
1. if
	- `if(조건, 참인 경우, 거짓인 경우)` 
``` sql
-- 도시의 인구가 100만이 넘으면 big city, 그렇지 않으면 small city를 scale 컬럼에 출력
select name, population, if(population >= 1000000, "big city", "small city") as scale
from city
having scale = "small city"
order by population desc
```
2. ifnull
	- `ifnull(컬럼이름, 디폴트 데이터)` 
``` sql
-- 독립연도가 없는 데이터를 0으로 출력
select indepyear, ifnull(indepyear, 0)
from country 
```
3. case when then else end
	- python의 if문과 비슷하게 사용 
	- `case when 조건 then 결과 else 결과 end`
		- `when, then`은 반복 가능 	
```sql
-- 나라별로 인구 10억 이상/1억~10억/1억 이하를 "big, medium, small"로 표시
select name, population
, case 
    when population > 1000000000 then "big"
    when population > 100000000 then "medium"
    else "small"
end as scale
from country
having scale = "medium"
order by population desc
```

### 3. Date Format
``` sql
use sakila
select date_format(payment_date, "%Y-%m") as monthly, sum(amount)
from payment
group by monthly
```

### 4. Join
test1 database와 user table, addr table 생성
``` sql
use test1
CREATE TABLE user (
user_id int(11) unsigned NOT NULL AUTO_INCREMENT,
name varchar(30) DEFAULT NULL,
PRIMARY KEY (user_id)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

CREATE TABLE addr (
id int(11) unsigned NOT NULL AUTO_INCREMENT,
addr varchar(30) DEFAULT NULL,
user_id int(11) DEFAULT NULL,
PRIMARY KEY (id)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

INSERT INTO user(name)
VALUES ("jin"),
("po"),
("alice"),
("petter");

INSERT INTO addr(addr, user_id)
VALUES ("seoul", 1),
("pusan", 2),
("deajeon", 3),
("deagu", 5),
("seoul", 6);
```
1. Inner Join
  - 그냥 inner join을 사용할 경우 user의 5개 데이터에 addr의 4개 데이터를 각각 mapping해 20 row의 데이터 생성
  - `on`에 매칭시킬 컬럼을 지정할 경우 일치하는 데이터만 찾아서 join (두 테이블에 다 있는 데이터만 join)

```
select *
from user
inner join addr

select * 
from user
inner join addr
on user.user_id = addr.user_id
```
2. Left Join
```
select user.user_id, user.name, addr.addr 
from user
left join addr
on user.user_id = addr.user_id
```
3. Right Join
```
select user.user_id, user.name, addr.addr 
from user
right join addr
on user.user_id = addr.user_id
```

### 5. Union
- full outer join은 union을 사용
``` sql
select name
from user
union
select addr
from addr

-- union all을 쓰면 중복이 제거되지 않음
select name
from user
union all
select addr
from addr

-- union을 이용해서 full outer join : left join union right join
select  user.name, addr.addr 
from user
left join addr
on user.user_id = addr.user_id
union
select user.name, addr.addr 
from user
right join addr
on user.user_id = addr.user_id
```

### 6. Sub-query
- select, from, where 절 등에서 사용이 가능
``` sql
use world
# 전체 나라수, 도시수, 언어수를 하나의 row로 출력
select count(*) from country
select count(*) from city
select count(distinct(language)) from countrylanguage

select
(select count(*) from country) as country_count,
(select count(*) from city) as city_count,
(select count(distinct(language)) from countrylanguage) as language_count
from dual
	# from dual은 안 써줘도 ok
    
-- from
# 800만 이상이 되는 도시의 국가코드 이름, 도시인구수를 출력
select countrycode, name, population
from city
where population > 8000000

-- filtering을 먼저 한 후에 join 
	-- join할 때는 최대한 적은 데이터끼리 하는 것이 쿼리 성능 향상에 도움
select city.countrycode, city.name, country.name, city.population
from 
(
select countrycode, name, population
from city
where population > 8000000
) as city
join country
on city.countrycode = coutry.code

-- join을 한 후에 filtering
select city.countrycode, city.name, country.name, city.population
from city
join country
on city.countrycode = coutry.code
having city.population > 8000000

-- where절
# 800만 이상 도시의 국가코드, 국가이름, 대통령 이름을 출력
select code, name, headofstate 
from country
where code in (
	select countrycode from city where population > 8000000 
)
```

### 7. Index
```sql
use employees

explain
select *
from salaries
where salary > 60000 and to_date > "2000-01-01"
order by salary
limit 1000

create index salaries
on salaries (salary)
```

### 8. View
	- 가상의 테이블
	- 컬럼의 수정이나 인덱스 설정 같은 명령을 할 수 없음
```sql
use world

select *
from countrylanguage
join(
select country.code, country.name as country_name, city.name as city_name
from country
join city
on country.code = city.countrycode
) as s1
on s1.code = countrylanguage.countrycode

create view code_name as 
select country.code, country.name as country_name, city.name as city_name
from country
join city
on country.code = city.countrycode

select *
from countrylanguage
join code_name
on code_name.code = countrylanguage.countrycode
```



