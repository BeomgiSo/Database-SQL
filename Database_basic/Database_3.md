> 03. View
1. View란?
2. 여러 테이블에서 View활용
3. View 삭제

> 3.1 View란?
- `하나 이상의 테이블`에서 여러 정보를 토대로 만들어지는 `가상 테이블`
- 고객이 `자전거를 빌리려고 할 때` 어떤 정보(테이블)을 보여줘야 할까?
    - 자전거 정보를 담고 있는 bicycleInfo테이블(자전거ID, 자전거 타입, 자전거 연식 ...)
    - 고객이 자전거를 대여하는데 `불필요한 요소까지 포함되어 있다.`
- 자전거 테이블에서 필요한 정보만 추출하여 가상의 테이블 생성
- 자전거 테이블(자전거 ID,자전거 종류,자전거 이미지, 대여한 자전거 연식) -> 자전거 가상 테이블(자전거ID,자전거종류,자전거 이미지)
    - 고객에게는 자전거 가상 테이블을 제공 `보안성과 속도를 높일 수 있음`

```sql
CREATE VIEW '테이블 명' AS
SELECT 가져오고자하는 속성, 속성2 ...
FROM 가져오고가자 하는 속성의 테이블
(WHERE 등 사용가능)

-- 지시사항 1번을 참고하여 View를 생성하세요.
CREATE VIEW v_KickboardInfoForCustomer as
SELECT pk_kickboard_id, kickboard_kind, kickboard_image
FROM tb_KickboardInfo;

SELECT * FROM v_KickboardInfoForCustomer;
```


> 3.2 여러 테이블에서 View 활용
- 자전거 공유 사업을 시작하고 일주일이 지난후, 데이터 분석팀의 람쥐는 지난 일주일의 정보를 토대로 고객들이 어떤 자전거를 선호하는지 분석하려고한다.
- 람쥐는 데이터 분석을 위해 토리에게 다음과같은 자료를 요청했다.
    - 대여일자, 자전거 종류, 자전거 연식
- 어떻게 자료를 제공해 줄까?

- 대여 테이블과 자전거 테이블에 대한 권한 부여?
    - 불필요한 정보(자전거ID, 자전거 이미지)제공 및 `고객 정보가 제공되어 개인정보 노출 위험성 증가`

- View를 생성하여 제공?
    - `필요한 정보`만 선택해 가상 테이블로 제공, 불필요한 정보 및 고객 정보를 제외하여 제공할 수 있음

- 여러 테이블에서 뷰(View)생성 방법

```sql
CREATE VIEW '테이블 명' AS
SELECT 가져오고자하는 속성1,속성2
FROM 테이블1,테이블2...
(WHERE 사용가능)

-- 지시사항 1번을 참고하여 코드를 작성하세요.

CREATE VIEW v_KickboardInfoForAnalysis as
SELECT B.pk_rental_date,A.kickboard_kind,A.kickboard_year
FROM tb_KickboardInfo as A, tb_KickboardRental as B
WHERE A.pk_kickboard_id = B.fk_kickboard_id;

SELECT * FROM v_KickboardInfoForAnalysis;
```

> 3.3 View 삭제
- 데이터 분석팀의 다라미가 데이터 분석이 완료되었다고 한다.
- 데이터를 어떻게 처리할까?
- View는 실제 존재하지 않는 가상의 테이블 -> 해당 테이블을 삭제하더라도 원본 테이블에는 영향이 없다

- 뷰(삭제)
```sql
DROP VIEW 삭제하고자 하는 View 명
```
