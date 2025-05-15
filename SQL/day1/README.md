## 문제 1: 이름이 있는 동물의 아이디

https://school.programmers.co.kr/learn/courses/30/lessons/59407

- 동물 보호소에 들어온 동물 중, 이름이 있는 동물의 ID를 조회하는 SQL 문을 작성 (이름이 없으면 NULL로 표시됨)
- 단, ID는 오름차순 정렬

### 코드:
```sql
SELECT ANIMAL_ID
FROM ANIMAL_INS
WHERE NAME IS NOT NULL
```

## 문제 2: 역순 정렬하기

https://school.programmers.co.kr/learn/courses/30/lessons/59035

- 동물 보호소에 들어온 모든 동물의 이름과 보호 시작일을 조회하는 SQL문을 작성
- 이때 결과는 ANIMAL_ID 역순으로 정렬

### 코드:
```sql
SELECT NAME, DATETIME
FROM ANIMAL_INS
ORDER BY ANIMAL_ID DESC
```

## 문제 3: 중복 제거하기

https://school.programmers.co.kr/learn/courses/30/lessons/59408

- 동물 보호소에 들어온 동물의 이름은 몇 개인지 조회하는 SQL 문을 작성
- 이때 이름이 NULL인 경우는 집계하지 않으며 중복되는 이름은 하나로 계산

### 코드:
```sql
SELECT COUNT(DISTINCT NAME)
FROM ANIMAL_INS
WHERE NAME IS NOT NULL
```

## 문제 4: 동물의 아이디와 이름

https://school.programmers.co.kr/learn/courses/30/lessons/59403

- 동물 보호소에 들어온 모든 동물의 아이디와 이름을 ANIMAL_ID순으로 조회하는 SQL문을 작성

### 코드:
```sql
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
ORDER BY 1
```

## 문제 5: 동물 수 구하기

https://school.programmers.co.kr/learn/courses/30/lessons/59406

- 동물 보호소에 동물이 몇 마리 들어왔는지 조회하는 SQL 문을 작성

### 코드:
```sql
SELECT COUNT(*)
FROM ANIMAL_INS
```

  
