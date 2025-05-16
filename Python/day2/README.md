## 문제 1: 나이 출력

https://school.programmers.co.kr/learn/courses/30/lessons/120820

**문제 설명**: 2022년 기준으로 주어진 나이(age)를 이용해 출생 연도 계산

**제한 사항**: 0 < age ≤ 120 (나이는 태어난 연도에 1살, 매년 1월 1일마다 1살씩 증가)

## 풀이 접근
- ( 나이(age) - 1 )은 태어난 후 경과한 연수
- 출생 연도 = 2022 - (age - 1) = 2023 - age

## 코드:

```python
def solution(age):
    return 2023-age
```

## 문제 2: 숫자 비교하기 

https://school.programmers.co.kr/learn/courses/30/lessons/120807

**문제 설명**: 정수 num1과 num2가 매개변수로 주어질 때, 두 수가 같으면 1 다르면 -1을 retrun하도록 solution 함수를 완성

**제한 사항**: 0 ≤ num1 ≤ 10,000, 0 ≤ num2 ≤ 10,000

## 코드:

```python
def solution(num1, num2):
    if not (0 <= num1 <= 10000 and 0 <= num2 <= 10000):
        print("입력 값이 제한 범위를 벗어났습니다.")
        return None
    return 1 if num1==num2 else -1
```

* 대입 연산자(=)와 비교 연산자(==) 구분
* 삼항 연산자(한 줄로 조건에 따라 값 선택)
```python
값1 if 조건 else 값2
```

## 문제 3: 각도기

https://school.programmers.co.kr/learn/courses/30/lessons/120829 

**문제 설명**: 각 angle이 매개변수로 주어질 때 예각일 때 1, 직각일 때 2, 둔각일 때 3, 평각일 때 4를 return하도록 solution 함수를 완성

- 예각 : 0 < angle < 90
- 직각 : angle = 90
- 둔각 : 90 < angle < 180
- 평각 : angle = 180

**제한 사항**: 0 < angle ≤ 180 (angle은 정수)

## 코드:

```python
def solution(angle):
    if not (0 < angle <= 180):
        raise ValueError("입력 값이 제한 범위를 벗어났습니다.")
    if 0 < angle < 90:
        return 1  # 예각
    elif angle == 90:
        return 2  # 직각
    elif 90 < angle < 180:
        return 3  # 둔각
    else:
        return 4  # 평각
```

* raise ValueError 사용하는 이유
- 잘못된 입력 시 None 반환 대신 예외를 발생시키면 문제를 즉시 인식하고 디버깅 할 수 있어 더 안전하다.

## 문제 4: 짝수의 합 

https://school.programmers.co.kr/learn/courses/30/lessons/120831

**문제 설명**: 정수 n이 주어질 때, n이하의 짝수를 모두 더한 값을 return 하도록 solution 함수를 작성

**제한 사항**: 0 < n ≤ 1000

## 풀이 접근
- range(2, n+1, 2) : 2부터 n까지 2씩 증가하는 수열 생성

## 코드:

```python
def solution(n):
    if not (0 < n <= 1000):
        raise ValueError("입력 값이 제한 범위를 벗어났습니다.")
    return sum(range(2, n + 1, 2))
```

## 문제 5: 배열의 평균값

https://school.programmers.co.kr/learn/courses/30/lessons/120817

**문제 설명**: 정수 배열 numbers가 매개변수로 주어질 때, numbers의 원소의 평균값을 return하도록 solution 함수를 완성

**제한 사항**: 0 ≤ numbers의 원소 ≤ 1,000, 1 ≤ numbers의 길이 ≤ 100 (정답의 소수 부분이 .0 또는 .5인 경우만 입력으로 주어진다.)

## 풀이 접근
- sum(numbers) / len(numbers)로 합계 / 개수를 계산하여 평균 구하기

## 코드:

```python
def solution(numbers):
    return sum(numbers) / len(numbers)
```
