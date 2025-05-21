## 문제 1: 입양 시각 구하기(1)

https://school.programmers.co.kr/learn/courses/30/lessons/59412

- 보호소에서는 몇 시에 입양이 가장 활발하게 일어나는지 알아보기
-  09:00부터 19:59까지, 각 시간대별로 입양이 몇 건이나 발생했는지 조회하는 SQL문을 작성
- 이때 결과는 시간대 순으로 정렬

## 코드:
```sql
SELECT HOUR(DATETIME) HOUR, COUNT(*) COUNT
FROM ANIMAL_OUTS
WHERE HOUR(DATETIME) BETWEEN 9 AND 19
GROUP BY 1
ORDER BY 1
```

## 문제 2: 진료과별 총 예약 횟수 출력하기

https://school.programmers.co.kr/learn/courses/30/lessons/132202

- APPOINTMENT 테이블에서 2022년 5월에 예약한 환자 수를 진료과코드 별로 조회하는 SQL문을 작성
- 이때, 컬럼명은 '진료과 코드', '5월예약건수'로 지정
- 결과는 진료과별 예약한 환자 수를 기준으로 오름차순 정렬하고, 예약한 환자 수가 같다면 진료과 코드를 기준으로 오름차순 정렬

## 코드:
```sql
SELECT MCDP_CD '진료과코드', COUNT(*) '5월예약건수'
FROM APPOINTMENT
WHERE APNT_YMD LIKE '2022-05%'
GROUP BY 1
ORDER BY 2, 1
```

## 문제 3: 12세 이하인 여자 환자 목록 출력하기

https://school.programmers.co.kr/learn/courses/30/lessons/132201

- PATIENT 테이블에서 12세 이하인 여자환자의 환자이름, 환자번호, 성별코드, 나이, 전화번호를 조회하는 SQL문을 작성
- 이때 전화번호가 없는 경우, 'NONE'으로 출력
- 결과는 나이를 기준으로 내림차순 정렬하고, 나이 같다면 환자이름을 기준으로 오름차순 정렬

## 코드:
```sql
SELECT PT_NAME, PT_NO, GEND_CD, AGE, COALESCE(TLNO, 'NONE') TLNO
FROM PATIENT
WHERE GEND_CD = 'W' AND AGE <= 12
ORDER BY AGE DESC, PT_NAME
```

## 문제 4: 인기있는 아이스크림

https://school.programmers.co.kr/learn/courses/30/lessons/133024

- 상반기에 판매된 아이스크림의 맛을 총주문량을 기준으로 내림차순 정렬하고 총주문량이 같다면 출하 번호를 기준으로 오름차순 정렬하여 조회하는 SQL 문을 작성

## 코드:
```sql
SELECT FLAVOR
FROM FIRST_HALF
ORDER BY TOTAL_ORDER DESC, SHIPMENT_ID
```

## 문제 5: 자동차 종류 별 특정 옵션이 포함된 자동차 수 구하기

https://school.programmers.co.kr/learn/courses/30/lessons/151137

- CAR_RENTAL_COMPANY_CAR 테이블에서 '통풍시트', '열선시트', '가죽시트' 중 하나 이상의 옵션이 포함된 자동차가 자동차 종류 별로 몇 대인지 출력하는 SQL문을 작성
- 이때 자동차 수에 대한 컬럼명은 CARS로 지정하고, 결과는 자동차 종류를 기준으로 오름차순 정렬

## 코드:
```sql
SELECT CAR_TYPE, COUNT(*) CARS
FROM CAR_RENTAL_COMPANY_CAR
WHERE OPTIONS LIKE '%통풍시트%' OR OPTIONS LIKE '%열선시트%' OR OPTIONS LIKE '%가죽시트%'
GROUP BY CAR_TYPE
ORDER BY 1
```

- 잘못된 풀이
> SELECT CAR_TYPE, COUNT(*) CARS
> FROM CAR_RENTAL_COMPANY_CAR
> WHERE OPTIONS IN ('통풍시트', '열선시트', '가죽시트')
> GROUP BY CAR_TYPE
> ORDER BY 1
- OPTIONS IN ('통풍시트', '열선시트', '가죽시트') 이 조건은 OPTIONS 값 전체가 딱 하나의 값일 때만 동작
- 하지만 문제에서 OPTIONS 컬럼은 이런 형태 ( '가죽시트,열선시트,후방카메라', '스마트키,네비게이션,열선시트')
- 콤마로 구분된 문자열이기 때문에 '열선시트'라는 단어가 포함되어 있어도 부분 포함을 검사하지 않음 > 전체 문자열이 정확히 일치하는 경우만 잡음
- LIKE 조건으로 부분 포함 검사하기
