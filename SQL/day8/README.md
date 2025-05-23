## 문제 1: 보호소에서 중성화한 동물

https://school.programmers.co.kr/learn/courses/30/lessons/59045

- 보호소에서 중성화 수술을 거친 동물 정보를 알아보려고 한다. 보호소에 들어올 당시에는 중성화1되지 않았지만, 보호소를 나갈 당시에는 중성화된 동물의 아이디와 생물 종, 이름을 조회하는 아이디 순으로 조회하는 SQL 문을 작성
- 중성화1 : 중성화를 거치지 않은 동물은 성별 및 중성화 여부에 Intact, 중성화를 거친 동물은 Spayed 또는 Neutered라고 표시

## 코드:
```sql
SELECT I.ANIMAL_ID, I.ANIMAL_TYPE, I.NAME
FROM ANIMAL_INS I JOIN ANIMAL_OUTS O ON I.ANIMAL_ID = O.ANIMAL_ID
WHERE I.SEX_UPON_INTAKE LIKE 'intact%' AND (O.SEX_UPON_OUTCOME LIKE 'Spayed%' OR O.SEX_UPON_OUTCOME LIKE 'Neutered%')
ORDER BY 1
```

## 문제 2: 조건에 맞는 도서와 저자 리스트 출력하기

https://school.programmers.co.kr/learn/courses/30/lessons/144854

- '경제' 카테고리에 속하는 도서들의 도서 ID(BOOK_ID), 저자명(AUTHOR_NAME), 출판일(PUBLISHED_DATE) 리스트를 출력하는 SQL문을 작성
- 결과는 출판일을 기준으로 오름차순 정렬
- 주의사항 : PUBLISHED_DATE의 데이트 포맷이 예시와 동일해야 정답처리

## 코드:
```sql
SELECT B.BOOK_ID, A.AUTHOR_NAME, DATE_FORMAT(B.PUBLISHED_DATE, '%Y-%m-%d') PUBLISHED_DATE
FROM BOOK B JOIN AUTHOR A ON B.AUTHOR_ID = A.AUTHOR_ID
WHERE B.CATEGORY = '경제'
ORDER BY B.PUBLISHED_DATE
```

## 문제 3: 조건별로 분류하여 주문상태 출력하기 (*)

https://school.programmers.co.kr/learn/courses/30/lessons/131113

- FOOD_ORDER 테이블에서 2022년 5월 1일을 기준으로 주문 ID, 제품 ID, 출고일자, 출고여부를 조회하는 SQL문을 작성
- 출고여부는 2022년 5월 1일까지 출고완료로 이 후 날짜는 출고 대기로 미정이면 출고미정으로 출력
- 결과는 주문 ID를 기준으로 오름차순 정렬

## 코드1:
```sql
SELECT ORDER_ID, PRODUCT_ID, DATE_FORMAT(OUT_DATE, '%Y-%m-%d'),
       CASE WHEN OUT_DATE IS NULL THEN '출고미정'
            WHEN OUT_DATE <= DATE '2022-05-01' THEN '출고완료'
            ELSE '출고대기' END AS 출고여부
FROM FOOD_ORDER
ORDER BY ORDER_ID
```
- 출고여부를 판단하기 위한 조건을 SQL로 구현하려면 CASE WHEN 구문을 사용
- DATE '2022-05-01'은 Oracle 및 표준 SQL에서 날짜 상수를 나타내는 방법

## 코드2:
```sql
SELECT ORDER_ID, PRODUCT_ID, DATE_FORMAT(OUT_DATE, '%Y-%m-%d') OUT_DATE,
    IF(OUT_DATE IS NULL, '출고미정', IF(OUT_DATE <= '2022-05-01', '출고완료', '출고대기')) AS 출고여부
FROM FOOD_ORDER
ORDER BY ORDER_ID
```
- IF 구문도 사용 가능

## 틀린 코드:
```sql
SELECT ORDER_ID, PRODUCT_ID, DATE_FORMAT(OUT_DATE, '%Y-%m-%d') OUT_DATE,
       IF(DATE_FORMAT(OUT_DATE, '%Y-%m-%d')<='2022-05-01', '출고완료', '출고미정') '출고여부'
FROM FOOD_ORDER
ORDER BY 1
```
- 출고여부 기준이 3가지임을 파악 못함 (문제 잘 읽자)
- DATE_FORMAT()은 출력 포맷을 위한 것이고, 날짜 비교에는 OUT_DATE를 그대로 사용하는 것이 정확

## 문제 4: 성분으로 구분한 아이스크림 총 주문량

https://school.programmers.co.kr/learn/courses/30/lessons/133026

- 상반기 동안 각 아이스크림 성분 타입과 성분 타입에 대한 아이스크림의 총주문량을 총주문량이 작은 순서대로 조회하는 SQL 문을 작성
- 이때 총주문량을 나타내는 컬럼명은 TOTAL_ORDER로 지정

## 코드:
```sql
SELECT INGREDIENT_TYPE, SUM(TOTAL_ORDER) TOTAL_ORDER
FROM FIRST_HALF F JOIN ICECREAM_INFO I ON F.FLAVOR = I.FLAVOR
GROUP BY INGREDIENT_TYPE
ORDER BY SUM(TOTAL_ORDER)
```

## 문제 5: 루시와 엘라 찾기

https://school.programmers.co.kr/learn/courses/30/lessons/59046

- 동물 보호소에 들어온 동물 중 이름이 Lucy, Ella, Pickle, Rogan, Sabrina, Mitty인 동물의 아이디와 이름, 성별 및 중성화 여부를 조회하는 SQL 문을 작성
- 결과는 아이디 순으로 조회

## 코드:
```sql
SELECT ANIMAL_ID, NAME, SEX_UPON_INTAKE
FROM ANIMAL_INS
WHERE NAME IN ('Lucy', 'Ella', 'Pickle', 'Rogan', 'Sabrina', 'Mitty')
ORDER BY 1
```
