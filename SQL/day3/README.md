## 문제 1: 여러 기준으로 정렬하기

https://school.programmers.co.kr/learn/courses/30/lessons/59404

- 동물 보호소에 들어온 모든 동물의 아이디와 이름, 보호 시작일을 이름 순으로 조회하는 SQL문을 작성
- 단, 이름이 같은 동물 중에서는 보호를 나중에 시작한 동물을 먼저 보여주기

## 코드:
```sql
SELECT ANIMAL_ID, NAME, DATETIME
FROM ANIMAL_INS
ORDER BY NAME ASC, DATETIME DESC
```

## 문제 2: 이름에 el이 들어가는 동물 찾기

https://school.programmers.co.kr/learn/courses/30/lessons/59047

- 동물 보호소에 들어온 동물 이름 중, 이름에 "EL"이 들어가는 개의 아이디와 이름을 조회하는 SQL문을 작성
- 이때 결과는 이름 순으로 조회 (단, 이름의 대소문자는 구분하지 않는다.)

## 코드:
```sql
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
WHERE ANIMAL_TYPE = 'Dog' AND LOWER(NAME) LIKE '%el%'
ORDER BY 2
```

- 대소문자 구분을 무시하려면 LOWER() 함수를 사용하여 비교하는 것이 안전
* UPPER() > 대문자로 변환 / LOWER() > 소문자로 변환
- LOWER(NAME) LIKE '%el%' : 'el' 또는 'EL'이 포함된 모든 이름 찾음

## 문제 3: 나이 정보가 없는 회원 수 구하기

https://school.programmers.co.kr/learn/courses/30/lessons/131528

- USER_INFO 테이블에서 나이 정보가 없는 회원이 몇 명인지 출력하는 SQL문을 작성
- 이때 컬럼명은 USERS로 지정

## 코드:
```sql
SELECT COUNT(*) AS USERS
FROM USER_INFO
WHERE AGE IS NULL
```

## 문제 4: 가장 비싼 상품 구하기

https://school.programmers.co.kr/learn/courses/30/lessons/131697

- PRODUCT 테이블에서 판매 중인 상품 중 가장 높은 판매가를 출력하는 SQL문을 작성
- 이때 컬럼명은 MAX_PRICE로 지정

## 코드:
```sql
SELECT MAX(PRICE) AS MAX_PRICE
FROM PRODUCT
```

## 문제 5: NULL 처리하기

https://school.programmers.co.kr/learn/courses/30/lessons/59410

- 동물의 생물 종, 이름, 성별 및 중성화 여부를 아이디 순으로 조회하는 SQL문을 작성
- 이때 프로그래밍을 모르는 사람들은 NULL이라는 기호를 모르기 때문에, 이름이 없는 동물의 이름은 "No name"으로 표시

## 코드 1: COALESCE() : 모든 DBMS에서 사용가능
```sql
SELECT ANIMAL_TYPE, 
            COALESCE(NAME, 'No name') AS NAME, 
            SEX_UPON_INTAKE
FROM ANIMAL_INS
ORDER BY ANIMAL_ID
```

- COALESCE 함수: 첫 번째 인자가 NULL일 때 두 번째 인자를 반환 (모든 값이 NULL이면 NULL을 반환)
```sql
COALESCE(column1, column2, ... , columN)
```

## 코드 2: IFNULL(MySQL)
```sql
SELECT ANIMAL_TYPE, IFNULL(NAME, 'No name') AS NAME, SEX_UPON_INTAKE
FROM ANIMAL_INS
ORDER BY ANIMAL_ID
```

## 코드 3: NVL(Oracle)
```sql
SELECT ANIMAL_TYPE, NVL(NAME, 'No name') AS NAME, SEX_UPON_INTAKE
FROM ANIMAL_INS
ORDER BY ANIMAL_ID
```

- NVL 또는 ISNULL(표현식1, 표현식2) : 표현식1의 결과값이 NULL 이면 표현식2의 값을 출력

## 코드 4: IS NULL()
```sql
SELECT ANIMAL_TYPE, 
            CASE WHEN NAME IS NULL THEN 'No name' ELSE NAME END AS NAME, 
            SEX_UPON_INTAKE
FROM ANIMAL_INS
ORDER BY ANIMAL_ID
```
