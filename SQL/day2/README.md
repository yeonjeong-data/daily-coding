## 문제 1: 동명 동물 수 찾기

https://school.programmers.co.kr/learn/courses/30/lessons/59041

- 동물 보호소에 들어온 동물 이름 중 두 번 이상 쓰인 이름과 해당 이름이 쓰인 횟수를 조회하는 SQL문을 작성
- 이름이 없는 동물은 집계에서 제외하며, 결과는 이름 순으로 조회

## 코드:
```sql
SELECT NAME, COUNT(NAME) AS COUNT
FROM ANIMAL_INS
WHERE NAME IS NOT NULL
GROUP BY NAME
HAVING COUNT(NAME) >= 2
ORDER BY 1
```

- 'WHERE NAME IS  NOT NULL AND COUNT(NAME)>=2' 는 구문 오류
* WHERE 절에 집계 함수(COUNT)를 사용할 수 없음 -> HAVING 절 사용 (그룹화된 데이터에 조건 필터링)

- SQL 쿼리 작성 순서: SELECT > FROM > WHERE > GROUP BY > HAVING > ORDER BY

## 문제 2: 아픈 동물 찾기

https://school.programmers.co.kr/learn/courses/30/lessons/59036

- 동물 보호소에 들어온 동물 중 아픈 동물1의 아이디와 이름을 조회하는 SQL 문을 작성
- 결과는 아이디 순으로 조회

## 코드:
```sql
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
WHERE INTAKE_CONDITION = 'Sick'
```

## 문제 3: 상위 n개 레코드

https://school.programmers.co.kr/learn/courses/30/lessons/59405

- 동물 보호소에 가장 먼저 들어온 동물의 이름을 조회하는 SQL 문을 작성

## 코드:
```sql
SELECT NAME
FROM ANIMAL_INS
WHERE DATETIME = (SELECT MIN(DATETIME) FROM ANIMAL_INS)
```

## 문제 4: 최솟값 구하기

https://school.programmers.co.kr/learn/courses/30/lessons/59038

- 동물 보호소에 가장 먼저 들어온 동물은 언제 들어왔는지 조회하는 SQL 문을 작성

## 코드 1:
```sql
SELECT DATETIME
FROM ANIMAL_INS
WHERE DATETIME = (SELECT MIN(DATETIME) FROM ANIMAL_INS)
```

## 문제 5: 어린 동물 찾기

https://school.programmers.co.kr/learn/courses/30/lessons/59037

- 동물 보호소에 들어온 동물 중 젊은 동물1의 아이디와 이름을 조회하는 SQL 문을 작성
* 젊은 동물1: INTAKE_CONDITION이 Aged가 아닌 경우를 뜻함
- 결과는 아이디 순으로 조회

## 코드 1:
```sql
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
WHERE INTAKE_CONDITION <> 'Aged'
ORDER BY 1
```

- <>와 != 사용 가능한데, <>가 더 표준적 (Oracle에서는 != 대신 <> 만 사용 가능)
