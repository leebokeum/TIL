### mysql에서 Json 필드 사용하기

insert
~~~ sql
insert into employees(name, profile) values('신상일', json_object(
    'age', 28, 
    'gender', 'man', 
    '부서', '연구'
));

-- json_array
insert into employees(name, profile) values('은연수', json_object(
    'age', 29,
    'gender', 'woman',
    '부서', '개발',
    '자격증', json_array('CISA', 'PMP', 'CISSP')
    ));

-- JSON_QUOTE
-- 문자열에 특수 문자가 있을 경우 처리. 다음은 'n 을 입력하는 예제
SELECT JSON_QUOTE('Scott\'n tiger'), JSON_QUOTE('"null');
~~~


select
### JSON_Extract
- 컬럼에서 JSON 데이타를 추출하며 JSON Path 문법을 사용
~~~ sql
-- 부서가 개발인 직원 정보를 출력하는 예제
select id,name,json_extract(profile, '$."부서"')
 from employees 
 where json_extract(profile, '$."부서"') = '개발';

-- 이중 따옴표(double Quote) 없애기
-- 아래 쿼리를 실행하면 결과가 0 이 나오며 이유는 json_extract 가 결과에 "" 를 붙이기 때문
select id,name,json_extract(profile, '$."부서"')
 from employees 
 where json_extract(profile, '$."부서"') like '개%';

 -- 아래와 같은 구문을 평가하므로 결과가 0 이 나오게 된다.
 select '"개발"' like '개%';

 --  MySQL 의 "unquotes the extracted result" 연산자인 ->> 를 사용해서 Quote 를 제거해 주면된다.
 select id,name, profile ->> '$."부서"', json_extract(profile, '$."부서"')
 from employees 
 where profile ->> '$."부서"' like '개%';
~~~


### JSON_Replace
- JSON 컬럼에서 값을 치환해서 리턴
~~~ sql
-- age 필드의 값을 30으로 변경하는 예제
select id, name, json_replace(profile, '$.age', 30) 
from employees;
~~~


update
~~~ sql
Update
  employees as e
  inner join (
    select id, JSON_REPLACE(profile,
        '$.age', profile ->> '$.age' + 1 ,
        '$."부서"', concat(profile ->> '$."부서"', '부')
    ) as newProfile
    from employees as p
  ) as A on e.id = A.id
set e.profile = A.newProfile
~~~