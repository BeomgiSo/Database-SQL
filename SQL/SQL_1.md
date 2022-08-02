# 1. SQL 시작하기

## 1.1 SQL 이란?
- 데이터베이스란 ?
    - 여러사람이 `공유`해 사용할 목적으로 `통합`하여 관리하는 데이터의 모음
    - MariaDB, Amzon Redshift, Oracle DB등 많은 종류가 존재

- 데이터베이스란 무엇일까?
    - Maira DB, Amazone Redshift, Mongo DB등 세상에 존재하는 `모든` 데이터베이스에 대해 알아야할까? `No!`

- 데이터베이스에서 `검색 분석`에 사용되는 기본사용 방법은 `데이터베이스 종류과 상관없이 동일`
- S(structure) Q(Query) L(Language)의 약자로 데이터 베이스에 `접근`하고 `조작`하기 위한 표준 언어

> 쿼리 작성하기
```sql
DESC Employees;
```
명령 + 대상


## 1.2 테이블에서 데이터 검색하기
**사용되는 문법** : `SELECT FROM DISTINCT`

- 데이터베이스의 종류
    - 관계형 데이터베이스 
        - 관계형 데이터베이스는 SQL을 통해 제어가능
        - 하나이상의 테이블로 이루어지며 서로 연결된 데이터를 가지고 있음
    - 비관계형 데이터베이스
        - 추가하기


- 테이블의 구성요소
    - `Name` : 모든 테이블은 고유의 이름으로 구분 (스네이크 표기법)
    - `Record (레코드)` : 내용 값
    - `Column (컬럼)` : 속성, 주제, 제목 등등... ()

>테이블에서 데이터 가져오기
```sql
SELECT title,author 
FROM book;
```
- book 테이블에서 모든 책의 title과 author컬럼을 검색한다.
- SELECT (검색할 대상)
- FROM (테이블명)
- WHERE (조건)

```sql
SELECT *
FROM book;
```
- book Table에서 모든 데이터를 검색

> 같은 데이터 제거해주기 `(DISTINC)`
- DISTINCT 뒤에 `2개 이상의 컬럼`을 적으면, `한쪽 컬럼에서 중복`이 있어도 `다른 쪽 컬럼 값이 다르면 `다르게 취급한다.
```sql
SELECT DISTINC title,author
FROM book;
```
- 검색할 데이터 앞에 DISTINCT를 입력하여 사용
```sql
SELECT DISTINCT  제목
```
- 제목관련 속성만 구분
```sql
SELECT DISTINCT  제목,저자
```
- 제목 및 저자를 구분해서 표현

## 1.3 여러개의 조건을 추가하기
**사용되는 문법** : `WHERE`

> 여러개의 조건을 추가
- 비교연산자
- < , > ,<=,=>,= , !=
- WHERE 을통해 조건 표시

```sql
SELECT *
FROM score
WHERE korea>=90;
```
- score 테이블의 모든 컬럼에서 국어 성적이 90이상이 값검색

- 복합 조건 추가하기
- AND, && //  OR,|| // ,NOT !
- 복합조건 연산자 사용하여 검색

```sql
SELECT *
FROM score
WHERE korean >= 90 OR math>80;
```

- 기타연산자
- A BETWEEN 10 AND 20 : A가 10과 20 사이에 포함된 값
- A IN B : B에 A가 포함된 값
- A NOT IN B :  B에 A가 포함되지 않은 값

```sql
SELECT *
FROM score
WHERE math BETWEEN 80 AND 90
```

score 테이블에서 math 성적이 80과 90 사이의값을 검색 (math 80이상 90이하 값)

# 2 SQL로 데이터를 제어하는 DML(데이터 조작어)
- SQL 명령어 종류
    - DML(data manipulation language) : 데이터 조적어
    - DDL : 데이터 정의어
    - DCL : 데이터 제어어
    - TCL : 트렌젝션 제어어

## 2.1 테이블에서 유사한 값 찾기
**사용되는 문법** : `LIKE`

- 데이터에서 `유사한 값` 찾기 => 찾으려는 데이터가 기억이 나지 않을 때
    - 왕자 라는 단어가 들어간 책을 검색할때
    - 왕자로 시작하거나 끝나거나 중앙에 있는 책을 검색

> LIKE : 특정 문자가 포함된 문자열을 찾고 싶을 때 사용하는 명령
- LIKE 조건의 기본 문법

```sql
SELECT *
FROM book
WHERE title LIKE '%왕자' 
--- book이란 테이블에서 제목(title)이 '어린왕자'인 책을 검색
```

- `% : (와일드 카드)` '
- %왕자' '왕자'로 끝나는 책 검색
- '왕자%' : 왕자로 시작하는 책 검색
- %린왕%  : 린왕이 호함된 책을 검색

> 요약
- BETWEEM A AND B : A와 B를 포함한 값 사이
- in (list) => in (list A,list B, list C) => 찾으려는 데이터가 여러개 일때 사용하기 좋다.

## 2.2 데이터 정렬하기
**사용되는 문법** : `ORDER BY`,`DESC`,`ASC`
- 점수가 높은 순서대로 정렬하기

```sql
SELECT *
FROM score
ORDER BY math DESC
```
* socre 테이블에서 수학 값이 **큰** 데이터 부터 검색

```sql
SELECT *
FROM score
ORDER BY math ASC
```
* socre 테이블에서 수학 값이 **작은** 데이터 부터 검색

# 2.3 테이블에 데이터 삽입하기
**사용되는 문법** : `INSERT`
- 관계형 데이터베이스의 테이블에 값을 `저장`하는 명령

```SQL
INSERT INTO book(id,title,author,publisher)
VALUES ('3','햄릿','윌리엄 셰익스피어','엘리스 출판');
```
- 햄릿 이란 책 데이터를 book 테이블에 추가

- `컬럼을 명시하지 않으면 순서대로 값`을 삽입한다.

# 2.4 테이블의 데이터 수정하기
**사용되는 문법** : `UPDATE ->SET, WHERE`
- 이미 저장된 값을 수정하는 명령
```sql
UPDATE book
SET title = '돈키호테 1' -- 변경할 값
WHERE title = '돈키호테 '; -- 조건
```

- 책 제목이 돈키호테를 돈키호테1로 바꾼다

# 2.5 테이블의 데이터 삭제하기
**사용되는 문법** : `DELETE`
- 관계형 데이터베이스의 테이블에서 이미 저장된 값을 삭제하는 명령
```sql
DELETE
FROM book -- 테이블
WHERE title='돈키호테1'; --조건
```
- `where 조건이 없을시 모든 데이터를 삭제한다.`

# 3 SQL과 내장함수
> 함수
- 데이터 값 계산 및 조작 : 행 함수
- 행의 그룹 계산 및 요약 : 그룹 함수
- 열의 데이터 타입을 반환

**사용할 함수** : `COUNT, LIMIT, SUM & AVG, MAX & MIN`
## 3.1 COUNT
**사용되는 문법** : `COUNT`

- 몇 개일지 조회
- 검색한 결과 데이터의 개수를 가져오는 내장 함수 
- NULL인 함수는 제외한다.

```SQL
SELECT COUNT(id) FROM book;
```
- book 테이블 안에 있는 `id컬럼의 개수`를 검색

```SQL
SELECT COUNT(*) FROM book;
``` 
- `모든 데이터 검색` => 양이 많아지면 에러가걸림..
- DATA 크기 예측에 사용

## 3.2 LIMIT - 데이터의 일부만 보고싶다.
**사용되는 문법** : `LIMIT`

- 몇개만 뽑아서 조회하겠다.
- 즉 출력하고자 하는 데이터의 개수를 제한하는 명령

```SQL
SELECT * FROM book LIMIT 5;
-- book 테이블에서 데이터 5개만 가져와
SELECT * FROM book LIMIT 1,5;
-- book 테이블에서 데이터 2번째 데이터 부터 5개만 가져와
```


## 3.3 SUM & AVG
**사용되는 문법** : `SUM AVG`
- `SUM` :지정한 값을 모두 더하는 내장함수

```SQL
SELECT SUM(math) FROM grade;
```

- `AVG` :지정한 값의 평균을 구하는 내장함수
```SQL
SELECT AVG(math) FROM grade;
```


## 3.4 MAX & MIN
**사용되는 문법** : `MAX & MIN`


- `MAX` : 최대값을 구하는 내장함수
- 데이터의 문자형도 가능  ex) ㄱ,ㄴ,ㄷ => ㄷ

```SQL
SELECT MAX(math) FROM grade;
```

- `MIN` : 최소값을 구하는 내장함수
- 데이터의 문자형도 가능  ex) a,b,c => a

```SQL
SELECT MIN(math) FROM grade;
```