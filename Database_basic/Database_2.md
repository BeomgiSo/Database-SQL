> Database 정규화(Normalization)
1. 정규화란?
2. 1차 정규화
3. 2차 정규화
4. 3차 정규화

> 01. 정규화란?
- 테이블 간 `데이터 조작(삽입,수정,삭제)시 발생 할 수 있는 이상 현상을 줄이기 위해 하는 작업`
- 다양한 정규화 과정이 있다
    - 그러나 `1~3차 정규화를 진행하면 대부분의 이상현상을 없앨 수 있다.`

> 02. 1차 정규화(1NF)
- 1차 정규화 란 ? `각 속성 마다 값이 1개씩 존재`하도록 하는 과정(원자화)
- row data의 값들이 각각 1개만 가지도록 수정
- 삭제시 중복 제거를 피할 수 있다.
```sql
-- 현재 tb_CustomerInfo 테이블의 상태를 출력하는 코드입니다.
SELECT * FROM tb_CustomerInfo;

-- 지시사항 1번을 참고하여 1차 정규화에 맞춰 데이터를 추가하세요.

DELETE FROM tb_CustomerInfo;
INSERT INTO tb_CustomerInfo VALUES ('elice_rabbit');
INSERT INTO tb_CustomerInfo VALUES ('hatseller');
INSERT INTO tb_CustomerInfo VALUES ('dodo_bird');

```
> 03. 2차 정규화(2NF)
- 2차 정규화란? `복합키로 구성 되어 있을 때 고려`해야 하며, 모든 속성이 `완전 함수 종속`이 되도록 하는 작업
- 완전 함수 종속? A,B,C,D가 있을때 B가 A에 의해 종속되는 경우 B는 다른 내용(C,D)에 의해 종속 되지 않는 경우

- 다람쥐의 전화번호를 수정하기 위해 고객 테이블의 전화보를 수정, 그후 10월 02일 다람쥐의 전화번호를 확인해보면 변경된 전화번호를 얻을 수 있음

```sql
CREATE TABLE `tb_CustomerInfo_2NF` (
 `pk_customer_id` VARCHAR(15),
 `customer_name` VARCHAR(20),
 `customer_tel` VARCHAR(15),
 -- 지시사항 1번을 참고하여 속성을 추가해주세요.
 PRIMARY KEY(`pk_customer_id`)
);
CREATE TABLE `tb_KickboardRental_2NF` (
 `pk_rental_date` VARCHAR(20),
 `fk_pk_customer_id` VARCHAR(15),
 `kickboard_id` VARCHAR(5),
 `kickboard_kind` VARCHAR(5),
 `kickboard_image` VARCHAR(50),
 `kickboard_year` INT,
 -- 지시사항 2번을 참고하여 속성을 추가해주세요.
 PRIMARY KEY(`pk_rental_date`,`fk_pk_customer_id`),
 FOREIGN KEY(`fk_pk_customer_id`) REFERENCES `tb_CustomerInfo_2NF`(`pk_customer_id`)
);
INSERT INTO tb_CustomerInfo_2NF VALUES ('elice_rabbit', '엘리스 토끼', '010-1111-2222');
INSERT INTO tb_CustomerInfo_2NF VALUES ('hatseller', '모자장수', '010-2222-3333');
INSERT INTO tb_KickboardRental_2NF VALUES ('2020-10-01 11:00', 'elice_rabbit', 'E01', 'A', 'http://...', 2019);
INSERT INTO tb_KickboardRental_2NF VALUES ('2020-10-02 12:00', 'elice_rabbit', 'E02', 'B', 'http://...', 2020);
INSERT INTO tb_KickboardRental_2NF VALUES ('2020-10-02 12:00', 'hatseller', 'E01', 'A', 'http://...', 2019);
INSERT INTO tb_KickboardRental_2NF VALUES ('2020-10-02 14:00', 'hatseller','E03', 'A', 'http://...', 2019);
```

> 04. 3차 정규화(3NF)
- 테이블 내에서 `이행적 요소를 제거`하는 작업
- `TABLE을 잘 나눠` 이행 적인 현상을 제거해 준다.
- 자전거의 수정하기위해 자전거 테이블의 종류를 수정, 대여 자전거에서 E01의 자잔거 종류 조회 시 동일하게 변경된 값을 확인할 수 있다.