## 문제 1: 이름이 없는 동물의 아이디

https://school.programmers.co.kr/learn/courses/30/lessons/59039

- 동물 보호소에 들어온 동물 중, 이름이 없는 채로 들어온 동물의 ID를 조회하는 SQL 문을 작성
- 단, ID는 오름차순 정렬

## 코드:
```sql
SELECT ANIMAL_ID
FROM ANIMAL_INS
WHERE NAME IS NULL
ORDER BY 1
```

## 문제 2: 조건에 맞는 회원수 구하기

https://school.programmers.co.kr/learn/courses/30/lessons/131535

- USER_INFO 테이블에서 2021년에 가입한 회원 중 나이가 20세 이상 29세 이하인 회원이 몇 명인지 출력하는 SQL문을 작성

## 코드:
```sql
SELECT COUNT(*) USERS
FROM USER_INFO
WHERE YEAR(JOINED) = 2021 AND AGE BETWEEN 20 AND 29
```

* 첫 시도에는 이렇게 작성했는데, 오류가 났고 그 이유를 파악해보았다.
SELECT COUNT(AGE BETWEEN 20 AND 29) USERS
FROM USER_INFO
WHERE YEAR(JOINED) = '2021'

> - YEAR() 함수는 '정수' 형태의 연도를 반환하므로 WHERE YEAR(JOINED) = 2021 이라 작성해야 한다.
> - SELECT COUNT(AGE BETWEEN 20 AND 29) USERS의 경우, AGE BETWEEN 20 AND 29 조건이 참(1) 또는 거짓(0)인 행의 개수를 세려고 시도 > 문제에서 원하는 것은 '해당 조건을 만족하는 회원의 수'이므로 COUNT(*)를 사용하여 WHERE 절의 조건을 만족하는 모든 행의 개수를 세어야 한다.

## 문제 3: 중성화 여부 파악하기

https://school.programmers.co.kr/learn/courses/30/lessons/59409

- 동물의 아이디와 이름, 중성화 여부를 아이디 순으로 조회하는 SQL문을 작성
- 이때 중성화가 되어있다면 'O', 아니라면 'X'라고 표시

- 참고)
- 'Neutered'(주로 수컷 중성화), 'Spayed'(주로 암컷 중성화)
- 'Intact' (중성화되지 않음)

## 코드:
```sql
SELECT ANIMAL_ID, NAME,
       CASE WHEN SEX_UPON_INTAKE LIKE 'Neutered%' OR SEX_UPON_INTAKE LIKE 'Spayed%' THEN 'O' ELSE 'X' END AS "중성화"
FROM ANIMAL_INS
ORDER BY 1
```

## 문제 4: 카테고리 별 상품 개수 구하기

https://school.programmers.co.kr/learn/courses/30/lessons/131529

- PRODUCT 테이블에서 상품 카테고리 코드(PRODUCT_CODE 앞 2자리) 별 상품 개수를 출력하는 SQL문을 작성
- 결과는 상품 카테고리 코드를 기준으로 오름차순 정렬

## 코드:
```sql
SELECT (SUBSTR(PRODUCT_CODE, 1, 2)) 'CATEGORY', COUNT(*) 'PRODUCTS'
FROM PRODUCT
GROUP BY 1
ORDER BY 1
```

## 문제 5: 고양이와 개는 몇 마리 있을까

https://school.programmers.co.kr/learn/courses/30/lessons/59040

- 동물 보호소에 들어온 동물 중 고양이와 개가 각각 몇 마리인지 조회하는 SQL문을 작성
- 이때 고양이를 개보다 먼저 조회

## 코드:
```sql
SELECT ANIMAL_TYPE, COUNT(*) count
FROM ANIMAL_INS
WHERE ANIMAL_TYPE IN ('Cat', 'Dog')
GROUP BY 1
ORDER BY 1
```
