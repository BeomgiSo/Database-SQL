# 4. SQL 다수의 테이블 제어하기

## 4.1 데이터 그룹짓기
**사용되는 함수 :**  `GROUP BY`

- `데이터의 컬럼`과 `함수를 통해` 특정 값을 추출하는데에 사용된다.
- `SUM AVG COUNT MAX MIN`를 활용하면 더욱 효과적으로 사용할 수 있다.

- `회원들이 책을 몇번 대여`했는지 알 수 있는방법>
```sql
SELECT user_id, COUNT(컬럼명) -- 명령 + 검색할 컬럼
FROM rental -- 테이블
GROUP BY user_id ; -- 그룹의 기준 컬럼
```
- `user_id가` `같은 열`에서 컬럼의 내용을 Count 값 출력
    
```sql
SELECT user_id, SUM(컬럼명) -- 명령 + 검색할 컬럼
FROM rental -- 테이블
GROUP BY user_id ; -- 그룹의 기준 컬럼
```
- user_id가 같은 열에서 컬럼의 내용을 다 더한 값을 출력

- GROUP BY 활용 예시
```sql
SELECT user_id,SUM(컬럼명) FROM rental GROUP_BY user_id;
-- user_id가 동일한 같은열에서 컬럼의 내용을 다 더한값
SELECT user_id,AVG(컬럼명) FROM rental GROUP_BY user_id;
-- user_id가 동일한 같은열에서 컬럼의 내용을 평균값
SELECT user_id,MAX(컬럼명) FROM rental GROUP_BY user_id;
-- user_id가 동일한 같은열에서 컬럼의 내용의 가장 큰 값
SELECT user_id,MIN(컬럼명) FROM rental GROUP_BY user_id;
-- user_id가 동일한 같은열에서 컬럼의 내용의 가장 작은 값
```


---
## 4.2 데이터 그룹에 조건 적용하기 - GROUP BY 절에 조건을 부여하고 싶다면?
**사용되는 함수 :**  `GROUP BY, HAVING`

```SQL
SELECT user_id, COUNT(*)
FROM rental
GROUP BY user_id
HAVING COUNT(user_id) >1;
```
- rental 테이블에서 user_id가 1개 초과의 데이터가 몇 개 있는지 검색한다.

---

## 4.3 두개의 데이터 그룹에서 조회하기
**사용되는 함수 :**  `INNER JOIN`

- 두 테이블의 정보를 한번에 조회할 수 있다.

```sql
SELECT *
FROM rental
INNER JOIN user; -- 연결한 테이블
```


## 4.4 조건을 적용해 두개의 테이블 조회하기
- inner join을 통해 연결된 테이블에 cal1 과 cal2와 일치하는 값들만 조회하고싶다.
**사용되는 함수 :**  `INNER JOIN, ON`

```sql
SELECT *
FROM rental
INNER JOIN user
ON user.id = rental.user_id;  -- 연결한 조건 컬럼
```

## 4.5 LEFT JOIN
**사용되는 함수 :**  `LEFT JOIN, ON`

- 대여기록이 없는 회원도 포함하여 데이터를 출력 하고싶다.
- 왼쪽 테이블의 모든 값을 포함하여 연결하기
```sql
SELECT *
FROM user
LEFT JOIN rental
ON user.id = rental.user_id;
```

- `user 테이블을 모두 출력`하되 모든 `user테이블의 user_id와 rental테이블의 id`가 겹치도록 합친다.
- `inner join은 두 데이터 중 겹치`는 부분만 출력
- `left join은 왼쪽 데이터와 겹치는 부분`을 출력

## 4.6 RIGHT JOIN
**사용되는 함수 :**  `RIGHT JOIN, ON`
```sql
SELECT *
FROM user
RIGHT JOIN rental
ON user.id=rental.user_id;
```

- rental 테이블을 모두 출력하되 모든 rental 테이블의 user_id와  user테이블의 id가 겹치도록 합친다.
- `right join` : 오른쪽 데이터와 겹치는 부분을 출력

---
# 5.서브쿼리

## 5.1 서브쿼리
- 정의 : `하나의 쿼리안`에 포함된 또 하나의 `쿼리` , 메인 쿼리가 서브쿼리를 포함하는 `종속적인 관계`
    - `알려지지 않은 기준`을 이용한 검색에 유용
    - 메인 쿼리가 실행되기 `이전에 한번만 실행`
    - 한문장에서 `여러번 사용가능`

> 기존의 검색 방법
```sql
SELECT * FROM employee
WHERE 급여>25000;
```

- `ramg`의 급여가 25000일때, `ramg 사원의 급여`를 알고 있는 상태에서 더 높은 급여를 받는 사원을 조회

> 서브쿼리의 예시

```sql
SELECT * FROM employee
WHERE 급여 >
(SELECT 급여 FROM employee WHERE 이름='ramg')
```
- ramg의 급여를 알지 못해도 검색이 가능

- 조건
    1. 서브쿼리는 ***`괄호와 함께`*** 사용되어야 한다.
    1. 서브쿼리 `안에서는 ORDER BY절은 사용할 수 없다.`
    1. 서브쿼리는 `연산자(>,=,<)`의 오른쪽에 사용되어야 한다.
    1. 서브쿼리는 `오로지 SELECT문`으로 작성할 수 있다.

## 5.2 반환에 따른 분류
- `단일 행 서브쿼리`의 정의
    - 결과가 `한 행만 나오는 서브쿼리`, 서브쿼리가 결과를 `1개의 값만 반환`하고, 이 결과를 `메인 쿼리로 전달`하는 쿼리

```sql
SELECT * FROM employee
WHERE 급여>
(SELECT 급여 FROM employee WHERE 사원번호 = 1);
```
- `사원번호는 기본적으로 1개만 있으므로` 한개의 행만 반환함 = `단일행`
- 결과가 한 행만 나오는 단일 행 서브쿼리와는 다르게 `서브쿼리가 2개 이상 반환`하고, 이결과를 메인 쿼리로 전달하는 쿼리 (ex 키가 160이상인사람)

|기호|뜻|
|---|---|
|=|같다|
|<>|같지 않다|
|>|크다|
|>=|크거나 같다|
|<|작다|

- `다중 행 서브쿼리`
    - 결과가 한 행만 나오는 단일 행 서브쿼리와 다르게 `서브쿼리가 결과를 2개 이상 반환`하고, 이결과를 메인 쿼리로 전달하는 쿼리

```sql
SELECT * FROM employee
WHERE 급여 IN (SELECT max(급여) FROM employee GROUP BY 부서번호);
```
1. IN : `하나라도 만족`하면 반환
1. ANY : `하나라도 만족하면` 반환 `비교연산 가능`
1. ALL : `모두 만족하면 반환` 비교 연산 가능.


- 예시
- 1 in (1,2,3,4) - True 
- 10 < any(1,2,3,4) - 최대값을 찾아라 4 -> FALSE
- 99 >= ALL(99,100,101) - 101 FALSE
```sql
-- salaries 테이블에서 from_date가 2000-12-31 이전인 사람들의 급여 중 하나의 급여 보다 더 적은 급여를 받은 직원의 급여 정보를 모두 출력해보세요.

SELECT * FROM salaries WHERE salary < any (SELECT salary FROM salaries WHERE from_date <'2000-12-31');

-- salaries 테이블에서 from_date가 2000-12-31 이전인 사람들의 급여 중 모든 급여보다 적은 급여를 받은 직원의 급여 정보를 모두 출력해보세요.

SELECT * FROM salaries WHERE salary < all (SELECT salary FROM salaries WHERE from_date <'2000-12-31');
```

> 스칼라 서브쿼리
- 일반적으로 서브쿼리는 `WHERE절에` 사용된다.
- `SELECT`절에서 사용하는 서브쿼리를 스칼라 서브쿼리라하고 오로지 한 행만 반환한다. 마치 JOIN을 사용한것과 같은 결과를 나타내지만 계산속도가 상당히 올라간다는 것을 알 수 있다.
```sql
-- salaries 테이블에서 직원 번호(emp_no)과 평균급여(avg_salary) 두 가지를 검색합니다.
-- 평균 급여는 SELECT 절에서 서브쿼리를 이용해 직접 계산하며 별칭을 avg_salary로 지정합니다.
-- 중복 없이 검색하기 위해 DISTINCT 를 이용하세요.
-- salaries 테이블에서 직원 번호와 한 직원의 평균 급여를 중복없이 출력해보세요.
select * from salaries;

-- select distinct emp_no, avg(salary) from salaries;
select distinct emp_no,
(
select avg(salary)
from salaries as A
where A.emp_no = B.emp_no) as avg_salary
from salaries as B;

```