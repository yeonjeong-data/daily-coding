## 문제 1: 오랜 기간 보호한 동물(1)

https://school.programmers.co.kr/learn/courses/30/lessons/59044

- 아직 입양을 못 간 동물 중, 가장 오래 보호소에 있었던 동물 3마리의 이름과 보호 시작일을 조회하는 SQL문을 작성
- 이때 결과는 보호 시작일 순으로 조회

## 접근 방식
- 입양을 가지 못한 동물 중 보호소에 가장 오래 있었던 3마리를 조회하려면, ANIMAL_INS 테이블에 있는 동물 중 ANIMAL_OUTS에 존재하지 않는 (ANIMAL_ID 기준) 데이터 찾기

## 코드:
```sql
SELECT I.NAME, I.DATETIME
FROM ANIMAL_INS I LEFT JOIN ANIMAL_OUTS O ON I.ANIMAL_ID = O.ANIMAL_ID
WHERE O.ANIMAL_ID IS NULL
ORDER BY I.DATETIME
LIMIT 3
```

## 틀린 코드
```sql
SELECT I.NAME, I.DATETIME
FROM ANIMAL_INS I LEFT JOIN ANIMAL_OUTS O ON I.ANIMAL_ID = O.ANIMAL_ID
ORDER BY I.DATETIME
LIMIT 3
```

- WHERE O.ANIMAL_ID IS NULL: 입양되지 않은 동물만 필터링
> LEFT JOIN된 ANIMAL_OUTS 테이블의 ANIMAL_ID가 NULL인 경우 (즉, 입양 기록이 없는 동물을 찾음)
- WHERE I.ANIMAL_ID IS NOT NULL 가 오류나는 이유 : 입양 여부를 판단할 수 없기 때문
> 단순히 ANIMAL_INS 테이블의 ANIMAL_ID가 NULL이 아닌 행을 필터링. 그런데 ANIMAL_INS에서 ANIMAL_ID는 절대 NULL이 될 수 없음 (NOT NULL 제약 조건 존재)
> 즉, 이 조건은 항상 참이므로, 모든 동물이 결과에 포함 → 입양을 갔는지 여부와는 아무 관련이 없음

## 문제 2: 카테고리 별 도서 판매량 집계하기

https://school.programmers.co.kr/learn/courses/30/lessons/144855

- 2022년 1월의 카테고리 별 도서 판매량을 합산하고, 카테고리(CATEGORY), 총 판매량(TOTAL_SALES) 리스트를 출력하는 SQL문을 작성
- 결과는 카테고리명을 기준으로 오름차순 정렬

## 코드:
```sql
SELECT B.CATEGORY, SUM(S.SALES) TOTAL_SALES
FROM BOOK B INNER JOIN BOOK_SALES S ON B.BOOK_ID = S.BOOK_ID
WHERE S.SALES_DATE LIKE '2022-01%'
GROUP BY B.CATEGORY
ORDER BY B.CATEGORY
```

## 틀린 코드
```sql
SELECT DISTINCT B.CATEGORY, COUNT(*) TOTAL_SALES
FROM BOOK B INNER JOIN BOOK_SALES S ON B.BOOK_ID = S.BOOK_ID
WHERE S.SALES_DATE LIKE '2022-01%'
GROUP BY B.CATEGORY
ORDER BY B.CATEGORY
```

- GROUP BY B.CATEGORY를 이미 사용했으므로 불필요하게 성능 저하함
- INNER JOIN은 JOIN으로 쓸 수 있음
- SALES 컬럼은 '판매 수량'을 나타내므로 단순히 행 수 ( COUNT(*) ) 가 아닌, **판매 수량의 합 ( SUM(SALES) )**을 계산해야 함

## 문제 3: 상품 별 오프라인 매출 구하기

https://school.programmers.co.kr/learn/courses/30/lessons/131533

- PRODUCT 테이블과 OFFLINE_SALE 테이블에서 상품코드 별 매출액(판매가 * 판매량) 합계를 출력하는 SQL문을 작성
- 결과는 매출액을 기준으로 내림차순 정렬, 매출액이 같다면 상품코드를 기준으로 오름차순 정렬

## 코드:
```sql
SELECT P.PRODUCT_CODE, SUM(P.PRICE*O.SALES_AMOUNT) SALES
FROM PRODUCT P JOIN OFFLINE_SALE O ON P.PRODUCT_ID = O.PRODUCT_ID
GROUP BY P.PRODUCT_CODE
ORDER BY 2 DESC, 1
```

## 문제 4: 있었는데요 없었습니다

https://school.programmers.co.kr/learn/courses/30/lessons/59043

- 보호 시작일보다 입양일이 더 빠른 동물의 아이디와 이름을 조회하는 SQL문을 작성
- 이때 결과는 보호 시작일이 빠른 순으로 조회

## 코드:
```sql
SELECT I.ANIMAL_ID, I.NAME
FROM ANIMAL_INS I JOIN ANIMAL_OUTS O ON I.ANIMAL_ID = O.ANIMAL_ID
WHERE I.DATETIME > O.DATETIME
ORDER BY I.DATETIME
```

## 문제 5: 오랜 기간 보호한 동물(2)

https://school.programmers.co.kr/learn/courses/30/lessons/59411

- 입양을 간 동물 중, 보호 기간이 가장 길었던 동물 두 마리의 아이디와 이름을 조회하는 SQL문을 작성
- 이때 결과는 보호 기간이 긴 순으로 조회

## 코드:
```sql
SELECT O.ANIMAL_ID, O.NAME
FROM ANIMAL_INS I JOIN ANIMAL_OUTS O ON I.ANIMAL_ID = O.ANIMAL_ID
ORDER BY DATEDIFF(O.DATETIME, I.DATETIME) DESC
LIMIT 2
```

## 맞는 코드지만, 덜 권장 코드
```sql
SELECT O.ANIMAL_ID, O.NAME
FROM ANIMAL_INS I INNER JOIN ANIMAL_OUTS O ON I.ANIMAL_ID = O.ANIMAL_ID
ORDER BY (O.DATETIME - I.DATETIME) DESC
LIMIT 2
```
- 일부 SQL 엔진에서는 DATETIME - DATETIME 연산이 정확히 어떤 결과형인지 다르게 처리할 수 있기 때문에, 명시적인 DATEDIFF 또는 TIMESTAMPDIFF 함수를 사용하는 것이 더 안전하고 명확함
