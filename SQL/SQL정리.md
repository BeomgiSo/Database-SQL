```sql
-- salaries 테이블에 있는 직원 번호를 중복 없이 출력해 봅니다.
select DISTINCT emp_no from salaries;
```

first_name이 'Chirstian' 또는 'Georgi' 이다.
gender가 남자이다.
hire_date가 '1986-06-26' 이 아니다.
연산자의 우선순위에 주의해야 합니다. ()를 활용해보세요.


```sql
-- 문제의 조건에 맞는 직원을을 출력합니다.
select * from employees where (first_name = "Chirstian" or first_name = "Georgi") and gender = "M" and hire_date != '1998-06-26';
```

```sql
DESC score;

-- 짜장면을 받을 수 있는 학생을 조회하는 쿼리를 작성해주세요.
select * from score where korean = 100 or english = 100 or math = 100 ;

-- 과자를 받을 수 있는 학생을 조회하는 쿼리를 작성해주세요.
select * from score where korean between 70 and 95 and english between 70 and 95 and math between 70 and 95 ;

```

```sql
-- 1980~1989년도에 입사한 직원을 검색하세요.
-- 1990~1999년도에 입사한 직원을 검색하세요.
select * from employees where hire_date between '1980-01-01' and '1989-12-31';
select * from employees where hire_date between '1990-01-01' and '1999-12-31';
```

```sql
-- 해당하는 작가가 쓴 책만 골라서 출력합니다.
select * from book where author in ('William Shakespeare','John Ronald Reuel Tolkien','Joanne Kathleen Rowling')
```

```sql
-- 아래에 제목이 The Little로 시작하는 책만 조회하는 쿼리를 작성해주세요.
select * from book where title like 'The Little%';
-- 아래에 제목에 and가 포함된 책만 조회하는 쿼리를 작성해주세요.
select * from book where title like '%and%';
-- 아래에 제목이 Rings로 끝나는 책만 조회하는 쿼리를 작성해주세요.
select * from book where title like '%Rings';
```

```sql
select user_id, count(*) from rental group by user_id;
```

```sql
-- salaries 테이블에서 emp_no과 직원별로 연봉을 받은 횟수를 조회해보세요.

select emp_no,count(*) from salaries group by emp_no;
```
```sql

-- 누가 몇권의 책을 빌려갔는지 조회해 봅시다.
-- 이때 두권 이상 빌린 사람들만 조회해 봅시다.

select user_id, count(*)
from rental
group by user_id
having count(user_id)>=2;
```

```sql
SELECT user_id, SUM(컬럼명) FROM rental GROUP BY user_id; -- user_id가 같은 열에서 컬럼의 내용을 다 더한 값을 출력
SELECT user_id, AVG(컬럼명) FROM rental GROUP BY user_id; -- user_id가 같은 열의 컬럼의 평균을 출력
SELECT user_id, MAX(컬럼명) FROM rental GROUP BY user_id; -- user_id가 같은 열중에서 해당 컬럼명이 가장 큰 값을 출력
SELECT user_id, MIN(컬럼명) FROM rental GROUP BY user_id; -- user_id가 같은 열중에서 해당 컬럼명이 가장 작은 값을 출력
```
```sql
SELECT * FROM emp;
-- 사원 번호가 7인 사원보다 나이가 어린 사원의 모든 컬럼을 조회 하는 쿼리를 작성하세요.
select * from emp where birthdate > (select birthdate from emp where empnum = 7)
```
연산자	연산자 뜻
IN	하나라도 만족하면 참
ANY	내부적으로 모두 or 연산을 함
ALL	내부적으로 모두 and 연산을 함
```sql
-- MANAGER 업무를 가진 사원 중 제일 높은 급여를 받는 사원보다 높은 급여를 받는 사원을 조회하는 쿼리를 작성해주세요.
select * from emp where sal > (select max(sal) from emp where job = 'manager');
```

``sql
-- 각 부서별 급여를 제일 많이 받는 사원의 월급을 받는 사원들을 조회하는 쿼리를 작성해주세요.
select * from emp where sal = any (select max(sal) from emp group by deptno)
```